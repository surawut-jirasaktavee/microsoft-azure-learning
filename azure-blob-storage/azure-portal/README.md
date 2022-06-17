# AZURE PORTAL
---

**Upload, download, and list blobs with the Azure portal**

## Prerequisites

To access Azure Storage need to be an `Azure subscription`. If don't have [Create one](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F)
How to create a storage account using:
- Azure portal
- Azure PowerShell
- Azure CLI

For create a storage account. [**Create Storage Account**](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal)

## Create a container

1. Navigate to your new storage accocunt in the Azure portal
2. In the left menu for the storage account;
   `Data storage` => `Containers`
3. Select **Container** button.
4. Type a name for your new container;
  - Must be lowercase
  - Must start with a letter or number
  - Can include only letters, numbers, and the dash(-) character
See more information about naming. [**Container and blob names**](https://docs.microsoft.com/en-us/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata)
5. Set the level of public access to the container (`Default is **Private**`)(no anonymous access).
6. Select **Create** for the container

## Upload a block blob

Block blobs are ideal for storing `text` and `binary` data in the cloud like files, images, and videos.

To upload a block blob to container in Azure portal;
1. In Azure portal, navigate to the container you created in the previos section.
2. Select the container to show a list of. blobs it contains. If container is new it won't yet contain any blobs.
3. Select the **Upload** the file system to find a fille to upload as a block blob.
4. Select the **Upload** button to upload the blob
5. Upload as many blobs as you want to upload in this way. The new blobs are now listed within the container.

## Download a block blob

To delete one or more blobs in the Azure portal;
1. In the Azure portal, navigate to the container.
2. Display the list of blobs in the container.
3. Use the checkbox to select one or more blobs from the list.
4. Select the **Delete** button to delete the selected blobs.
5. In the dialog, confirm the deletion

## Clean up resources

To remove all the resources that created need to delete the container;

1. In the Azure portal, navigate to the list of containers in your storage account.
2. Select the container to delete.
3. Select the **More** button (...) and select **Delete**.
4. Confirm
