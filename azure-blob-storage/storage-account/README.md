# CREATE A STORAGE ACCOUNT
---

An `Azure storage account` contains all of your **Azure Storage data obkects**: blobs, files, queues, and tables.
The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the
world over `HTTP` or `HTTPS`. 


**Create a storage account**

A storage account is an Azure Resource Manager resource. Resource Manager is the deployment and management service for Azure.
When you create a storage account, you have the two options:
- create a new resource group
- use an existing resource group

To create a storage account with **Azure CLI**

````Azure CLI
az group create \
--name <Your resource group name> \
--location <Your selected location>
````
