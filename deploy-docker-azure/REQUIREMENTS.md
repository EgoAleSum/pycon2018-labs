Pre-requisites for this lab

## Set up VS Code and Code on the demo machine

Clone the following repo and start VS Code in the repo:
```
https://github.com/qubitron/flask-webapp-quickstart
cd flask-webapp-quickstart
code .
```

VS Code installed with the following extensions:
 - Docker
 - Python
 - Azure

Azure subscription set up and logged into with VS Code.

The Azure CLI is installed on the command line

## Create Azure Resource Groups
Create the pyconlabs container registry, using the `pyconlabstemplate.json` ARM template OR by running:
`
az group create --name PyConLabs --location "South Central US"
az acr create --name pyconlabs --resource-group PyConLabs --location "South Central US" --sku Basic
az acr update --name pyconlabs --admin-enabled true
`

Note to beta testers: you can skip this part.

Create an empty DockerLab resource group, the user should only need access to this resource group. You can create it using the ```dockerlabtemplate.json``` file or by running the command:
```
az group create --name DockerLab --location "South Central US"
```


## Login to the Registry
Get the password by running:
`
az acr credential show -n pyconlabs
`

Run the following command:
`
docker login pyconlabs.azurecr.io
`

Use the username `pyconlabs`, and the password shown from the credential command. 

Note to beta testers: use pyconlabstest.azurecr.io instead, username is `pyconlabstest`, the password is currently `bpF1E7+bmyzxVIJFSK7KhPxNpfGmq9rK`

# Demo reset instructions
After each lab, delete the resource group "DockerLab" and re-create an empty one by running:
`
az group delete --name DockerLab --yes
az group create --name DockerLab --location "South Central US"
`



