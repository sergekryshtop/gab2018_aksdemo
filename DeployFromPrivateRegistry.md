# Deploy image from Private Registry

## Creating Kubernetes secret to access private registry.

As example, connecting AKS to ACR using secret

$query="join(' ', ['docker login $RegistryName.azurecr.io', '-u', username, '-p', passwords[0].value])"

az acr credential show -n $RegistryName `
--query $query `
--output tsv `
| cmd