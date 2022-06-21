# STORAGE ACCOUNT SETTINGS
---

A storage account defines a policy that applies to all the storage services.
For example:
- Specify the location
- Specify the way to accessible
- Specify the way to billed of subscription

The settings that are defined by storage account are:
- **Subscription**: The Azure subscription that will be billed for the services in the account.
- **Location**: The datacenter that will store the services in the account.
- **Performance**: Detemines the data services you can have in your storage account and the type of hardware disks used to store the data.
  * **Standard** allows you to have any data service(Blob, File, Queue, Table) and uses magnetic disk drives(HDD).
  * **Premium** provides more services for storing data
    * Storing unstructured object data as block blobs
    * Storing unstructure object data as append blobs
    * Specialized file storage used to store and create premium file shards
    * Use solid-state drives (SSD) for stored the data
- **Replication**: Determines the strategy used to make copies of your data to protect against hardware failure or natural disaster.
  * At a minimum Azure autimatically maintains the following:
    * Maintains `three copies` of your data within the datacenter associated with the storage account.
    * Replication is called redundant storage (LRS)
    * Guards against hardware failure but does not protect from an event that incapacitates the entire datacenter.
  * At upgrade version Azure will allow you to other options such as:
    * Geo-redundant storage (GRS) to replication at different datacenter across the world.
    * etc.
- **Acess tier**: Controls how quickly you will be able to access the blobs in a storage account.
  * **Hot** gives quicker access than Cool but will increase your cost. apply to blobs and serves as the default value for new blobs.
  * **Cool** vice versa from `Hot`. 
- **Secure transfer required**: A security feature that determines the supported protocols for access.
  * HTTPS for enabled requires
  * HTTP while disabled.
- **Vitual networks**: A security feature that allows inbound access requests only from virtual network that you specify.


A storage account represents a collection of settings like location, replication and subscription owner.
The settings above are the condition that you need or require for your data. 
Typically determined by:
* Data diversity 
  Organization of the generate data the differs in where it is consumed. how sensitive it is, which group pays the bills etc.
  * Region/Country
  * Performance
  * Compliance reasons
* Cost sensitivity
  A storage account by itself has no financial cost but the settings above that you choose for the account do influence the cost of services
  in the account. 
* Tolerance for management overgead
  Each storage account requires some time and attention from an administration to create and maintain. it also increases complexity for anyone
  who adds data yo your cloud storage. need to understand the purpose of each storage account for add new data to correct account.
  
We could use `Storage account` tools to obtain the performance and security that need while minimizing costs.
A typical strategy is to start with an analysis of your data and create partitions that shard characteristics like location,
billing, and replication strategy, and then crate one storage account for each partition.
