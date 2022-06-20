# CREATE A STORAGE ACCOUNT
---

An `Azure storage account` contains all of your **Azure Storage data obkects**: blobs, files, queues, and tables.
The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the
world over `HTTP` or `HTTPS`. 


## Create a storage account

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

For the `--location` parameter. you can retrieve a list of supported regions for your subscription with the
`az account list-locations` command.

````Azure CLI
az account list-locations \
--query "[].{Region:name}" \
--out table
````

After selected the create the resource group and location then create storage account with `az storage account create` command.

````Azure CLI
az storage account create \
--name <Your-storage-name> \
--resource-group <Your-resource-group> \
--location <Your selected location> \
--sku Standard_RAGRS <example> \
--kind StorageV2 <example>
````


## Delete a storage account

Deleting a storage account deletes the entire account, including all data in the account.
**Note**: Be sure to back up any data you want to save before delete the account.

````Azure CLI
az storage account delete \
--name <Your-storage-account> \
--resource-group <Your resource group name>
