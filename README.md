"# gab2018_aksdemo" 
# Deploying application to AKS demo scriptDeploying application to AKS demo script

## Preparing environments

### Preparing local invironment
*** Need to install Azure CLI to proxy access to AKS dashboard
1. Install Azure CLI
Find installation instructions on: (https://docs.microsoft.com/fi-FI/cli/azure/install-azure-cli?view=azure-cli-latest)

For Windows: (https://aka.ms/installazurecliwindows)

2. Install SSH client for Windows: Putty
(https://www.putty.org/)

### Setting up Linux VM
Follow following instructions to provision and setup Linux VM in Azure
[Setup Linux VM in Azure](./SetupLinuxVM.md)

## Demo

### Provisioning AKS Cluster
  
[Create Managed Kubernetes Cluster](./CreateAKS.md)

### Deploying sample application
  
[Deploy app to cluster](./DeployApp.md)

### Scaling AKS Cluster

* Add another node to the cluster  

az aks scale -n gab18aks -g gab18aks --node-count 2

* Open K8s Dashboard  

az aks browse -n gab18aks -g gab18aks

## Other 

* [How to copy SSH keys and K8s config from Azure Linux VM](./CopyFromLinuxVM.md)
* Additional reading: (https://azure.microsoft.com/en-ca/solutions/architecture/container-cicd-using-jenkins-and-kubernetes-on-azure-container-service/)

* [Create Azure Subscription](./CreatingAzureSubscription.md)