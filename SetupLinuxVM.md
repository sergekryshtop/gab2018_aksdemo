# Setup Linux VM in Azure

## Provisinging Linux VM in Azure

1. Create Resource Group

az group create --name gab2018 --location "westeurope"

2. Create Linux VM with DNS name

Replace <vm_name> with your unique name, for example: gablabskr  
Username: gab18usr  
Password: 'pa$$w0rd!.12345'  
  
az vm create --name <vm_name> --resource-group gab2018 --admin-username gab18usr --admin-password 'pa$$w0rd!.12345' --generate-ssh-keys --storage-sku Standard_LRS --image UbuntuLTS --size Standard_D1_v2 --public-ip-address-dns-name <vm_name>


3. SSH to VM: gab18usr@<vm_name>.westeurope.cloudapp.azure.com
For Windows use Putty.  



## Configuring VM (Ubuntu)

### installing CLI
(https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest)


AZ_REPO=$(lsb_release -cs)
echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
     sudo tee /etc/apt/sources.list.d/azure-cli.list
	 
sudo apt-key adv --keyserver packages.microsoft.com --recv-keys 52E16F86FEE04B979B07E28DB02C46DF417A0893

curl -L https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

sudo apt-get install apt-transport-https
sudo apt-get update && sudo apt-get install azure-cli




### Install docker

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
apt-cache policy docker-ce
sudo apt-get install -y docker-ce
sudo rm /usr/bin/docker-compose

sudo curl -L https://github.com/docker/compose/releases/download/1.20.0/docker-compose-`uname -s`-`uname -m` -o /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose


### Optionally install Mono

sudo apt-get install mono-complete --assume-yes

