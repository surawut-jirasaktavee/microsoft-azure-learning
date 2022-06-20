# AZURE STORAGE DATA SERVICES
---

The Azure Storage platform includes the following data services:
**NOTE**: each service is accessed through a storage account.

## [Blob storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)

`Azure Blob storage` is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing
massive amounts of unstructured data, such as text or binary data.

The Objects in Blob storage can be accessed from anywhere in the world via `HTTP` or `HTTPS`.

- Serving images or documents directly to browser.
- Storing files for distributed access.
- Streaming video and audio
- Storing data for backup and restore, disater recovery, and archiving.
- Storing data for analysis by an on-premises or Azure-hosted service.

## [Azure Files](https://docs.microsoft.com/en-us/azure/storage/files/storage-files-introduction)

`Azure Files` enables you to set up highly available network file shares. that can be acessed by using the standard **Server Message Block** (SMB) protocol. 

- Multiple VMs can share the same files with both read and write access.
- Can read the files using the REST interface or the storage client libraries.

## [Queue storage](https://docs.microsoft.com/en-us/azure/storage/queues/storage-queues-introduction)

The `Azure Queue` service is used to store and retrieve messages.
- Can be up to 64 KB in size.
- Can contain millions of messages.
- Generally used to store lists of messages to be processed asynchronously.

## [Azure Tables](https://docs.microsoft.com/en-us/azure/storage/tables/table-storage-overview)

`Azure Table` storage is now part of `Azure Cosmos DB`.

## [Azure Disks](https://docs.microsoft.com/en-us/azure/virtual-machines/managed-disks-overview)

An Azure managed disk is a **virtual hard disk** (VHD). The virtualized disk. It like a physical disk in an on-premises server. And store as a page blobs, which are a random IO storage object in Azure. 

It is an abstraction over page blobs, blob containers, and Azure storage accounts. With managed disks, all you have to do is provision the disk, and Azure takes care of the rest.



