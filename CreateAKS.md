# Provision AKS

## 1. Login to Linux VM via ssh
  
Use putty or ssh client.
You can enable port mapping and tunner from remote port 8001

## 2. Create resource group  

*** This step helps to verify that only AKS service is created in the group and Azure put all related resources to aditional resource group

az group create --name gab18aks --location westeurope


## 3. Create AKS cluster

Replace <CLUSTER_NAME> with desired unique name, i.e. gab18aks

az aks create --resource-group gab18aks --name <CLUSTER_NAME> --node-count 1 --generate-ssh-keys  --node-vm-size Standard_D1_v2  --dns-name-prefix <CLUSTER_NAME>


Verify cluster created and version of Kubernetes
  
az aks list -o table
  
## 4. Get K8s keys and config
  
az aks get-credentials --resource-group gab18aks --name <CLUSTER_NAME>
  
az aks get-versions --location westeurope --resource-group gab18aks --name <CLUSTER_NAME> -o table


## 5. Test connection to the management console
  
kubectl get nodes


## 6. Open Management Console

az aks browse -n <CLUSTER_NAME> -g gab18aks

  
  

## Upgrade Kubernetes cluster to version 1.9.2.
*** Execute later or in case of issue with credentials

* Get current version   
az aks list -o table  

* Upgrade  
  
az aks upgrade --resource-group gab18aks --name gab18aks --kubernetes-version 1.9.2 --yes


* Verify  
     
az aks list -o table


* Test 

kubectl get nodes



