# INTRODUCTION TO AZURE STORAGE
---
reference: [introduction to Azure Storage](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)


## What is a storage account?

`A storage account` is a container that groups a set of `Azure Storage services` together. Only data service from Azure Storage can be included in a storage account(Azure Blobs, Azure Files, Azure Queues, and Azure Tables). The following illustration shows a storage account containing several data services.

![Storage Account](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/azure-storage-account/images/2-what-is-a-storage-account.png)

## What is a storage account do?

1. Combining data services into a single storage account enables you to mangage them as a group. 
2. The settings you specify when you create the account, or any changes that you make after creation will apply to all services in the storage account.
3. Deleting a storage account will deletes all of the data stored inside it.

## What is about Other Azure data services?

Other Azure data services, such as `Azure SQL`, `Azure Cosmos DB` are managed as independent Azure resources and cannot be include in storage account. As illustration shows as following:

![Azure data service in/out storage account](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/azure-storage-account/images/2-typical-subscription-organization.png)


The `Azure Storage platform` is Microsoft's cloud storage solution for modern data storage scenarios.
They offer the following for a variety of data objects in the cloud:
- highly available
- massively
- scalable
- durable
- secure storage

Azure storage data objects are accessible from anywhere in the world over `HTTP` or `HTTPS` via `REST API`.
They also offer client library for developers building applications or services with `Python` as well.
For other libraries:
- .NET
- Java
- Python
- JavaScript
- C++
- Go

Or SDK tools like:
- Azure PowerShell
- Azure CLI

You can interacting with Azure Storage by user-interface tools:
- Azure portal
- Azure Storage Explorer 

## AZURE STORAGE TOPICS

- [CREATE STORAGE ACCOUNT](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/azure-storage-account/create-storage-account.md)
- [BENEFITS OF AZURE STORAGE](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/azure-storage-account/benefits.md)
- [AZURE STORAGE DATA SERVICES](https://github.com/surawut-jirasaktavee/microsoft-azure-learning/blob/main/azure-storage-account/azure-storage-data-services.md)
- [TYPES OF STORAGE ACCOUNTS](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview)
