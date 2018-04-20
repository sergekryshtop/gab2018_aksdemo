# Deploy Demo Application

Demo application is taken from (https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app)

## Building docker image

1. SSH to Linix VM

2. Clone application from GitHub  

git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
cd azure-voting-app-redis

3. Start locally 

docker-compose up -d

4. Test locally in browser 

(http://localhost:8080)


5. Stop containers

docker-compose stop
docker-compose down


## Create Azure Registry

Replace <ACR_NAME> with unique registry name (i.e. gab18acr).    


az acr create -n <ACR_NAME> -g gab2018 --sku Basic --admin-enabled true 

LOGIN_SERVER=$(az acr list -g gab2018 --query "[].{acrLoginServer:loginServer}" --output tsv)
echo $LOGIN_SERVER


## Pubish docker image to registry

1. Login to registry  

az acr create -n <ACR_NAME> -g gab2018 --sku Basic  
  
LOGIN_SERVER=$(az acr list -g gab2018 --query "[].{acrLoginServer:loginServer}" --output tsv)
echo $LOGIN_SERVER  
  
ACR_SECRET=$(az acr credential show -n <ACR_NAME> --query "passwords[0].value")  
  
echo $ACR_SECRET  
  
echo "$ACR_SECRET"| docker login -u gab18lab  --password-stdin $LOGIN_SERVER


2. Tag and Push image 

docker tag azure-vote-front $LOGIN_SERVER/azure-vote-front:v1
docker push $LOGIN_SERVER/azure-vote-front:v1


3. List images in registry 

az acr repository list --name gab18lab --output table

4. Test pull command  

docker pull $LOGIN_SERVER/azure-vote-front:v1


## Grant read access for AKS cluster to access registry  

Replace <AKS_NAME> with cluster name, for example: gab18aks

CLIENT_ID=$(az aks show -g gab18aks --name gab18aks --query "servicePrincipalProfile.clientId" --output tsv)
  
echo $CLIENT_ID  
  
ACR_ID=$(az acr show -n <ACR_NAME> -g gab2018 --query "id" --output tsv)
  
echo $ACR_ID

az role assignment create --assignee $CLIENT_ID --role Reader --scope $ACR_ID
  


 