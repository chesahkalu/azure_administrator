# Azure Storage

---

## Table of Contents


---

## Pre-requisites

- Understanding of Azure fundamentals
- An Azure account with an active subscription (Free tier is enough). Sign up or log in to your Azure account [here](https://azure.microsoft.com/en-us/free/)
- Azure Storage Explorer installed on your local machine. Download and install it from [here](https://azure.microsoft.com/en-us/features/storage-explorer/)

---

## Introduction

- Azure Storage is a service that you can use to store `files`, `messages`, `tables`, and other types of information. You use Azure Storage for applications like file shares. Developers use Azure Storage for working data. Working data includes websites, mobile apps, and desktop applications. Azure is `durable and highly available`, and also `encrypts` all data at rest.

- For VMs, you can use Azure storage as `Disks` and fully managed `Files`. 
- Unstructured data can be stored in `Blobs` and `Azure Data Lake Storage`
- Structured data can be stored in `Azure Table Storage` , `Azure SQL Database` and `Azure Cosmos DB`

---

### Azure Storage services

- **Azure Blob Storage**: Store and manage unstructured data as `Objects` or `Blobs`(Binary Large Objects). Blobs can be text or binary files, such as documents, media files, and application installers. They can also store data for backup, restore, disaster recovery, and archiving. Objects in Blob Storage can be accessed from anywhere in the world via `HTTP or HTTPS`. Users or client applications can access blobs via `URLs`, the Azure Storage REST API, Azure PowerShell, the Azure CLI, or an Azure Storage client library. The storage client libraries are available for multiple languages, including .NET, Java, Node.js, Python, PHP, and Ruby.
    - Blob storage stores in this hierarchy: `Storage Account -> Container -> Blob`. All accounts can have an ulimited number of containers and all containers can have an unlimited number of blobs.
    - `Configure a container` :
        1. Name: Must be unique within the storage account.
        2. The name can contain only lowercase letters, numbers, and hyphens.
        3. The name must begin with a letter or a number.
        4. The minimum length for the name is three characters.
        5. The maximum length for the name is 63 characters.
        6. Configure the access level for the container: `Private`(default), `Blob`(public read access for blobs only), `Container`(public read access for container and blobs).
    - `Blob access tiers`:
        1. `Hot`: Optimized for storing data that is accessed frequently.
        2. `Cool`: Optimized for storing data that is infrequently accessed and stored for at least `30` days.
        3. `Cold`: Optimized for storing data that is rarely accessed and stored for at least `90` days with flexible latency requirements.
        3. `Archive`: Optimized for storing data that is rarely accessed and stored for at least `180` days with flexible latency requirements.
    - `Blob lifecycle management`: In the Azure portal, you create lifecycle management policy rules for your Azure storage account by specifying several settings. For each rule, you create `If - Then` block conditions to transition or expire data based on your specifications
        1. Define rules to automatically transition blobs to a cooler storage tier `if` they have not been accessed for a specified number of days.
        2. Define rules to automatically delete blobs at the end of their lifecycle.
        3. Define rules to automatically delete previous versions of blobs.
        4. Define rules to automatically set the access tier of blobs.
    - `Blob Types`: 
        1. `Block Blobs`: Optimized for streaming and storing cloud objects, and are a good choice for storing documents, media files, backups, and other large binary objects.
        2. `Append Blobs`: Optimized for append operations, making them ideal for scenarios such as `logging` data from virtual machines.
        3. `Page Blobs`: Optimized for random read-write operations, making them ideal for scenarios such as VHDs.
    - `Uploading Blob`:
        


    



- **Azure Files**: Managed file shares in the cloud that are accessible via the `Server Message Block (SMB) protocol` and the `Network File System (NFS) protocol`. Azure file shares can be mounted concurrently by cloud or on-premises deployments of Windows, macOS, and Linux. Azure file shares can also be cached on Windows Servers with Azure File Sync for fast access near where the data is being used.

- **Azure Queue Storage**: A service for storing large numbers of `messages` that can be accessed from anywhere in the world via authenticated calls using `HTTP or HTTPS`. A single message can be up to `64 KB` in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.

- **Azure Table Storage**: A service that stores `structured NoSQL data` in the cloud, providing a key/attribute store with a schema-less design. Because Table Storage is schema-less `(non-relational)` it's easy to adapt your data as the needs of your application evolve. Access to Table Storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.

---

### Storage Replication

Azure Storage offers several types of replication, to ensure durability and high availability.  Azure Storage replication copies your data to protect from planned and unplanned events. These events range from transient hardware failures, network or power outages, massive natural disasters, and so on. The following are the types of replication available in Azure Storage:

**Locally redundant storage (LRS)**: Locally redundant storage maintains `three` copies of your data. LRS is replicated three times within a storage scale unit in a datacenter(a single`availability zone` in a region). LRS is designed to provide at least `99.999999999% (11 9's) durability of objects over a given year`. If a data center-level disaster occurs, such as fire or flooding, all replicas might be lost or unrecoverable. Despite its limitations, LRS can be appropriate in several scenarios. This can be good for `constantly changing data` , `non-critical data` that can be easily restored , region/zone data `restrictions`.

**Zone-redundant storage (ZRS)**: Zone-redundant storage maintains `three` copies of your data across three storage clusters(3 availability zones) in a single region.  `Each storage cluster is physically separated from the others and resides in its own availability zone providing higher durability than LRS. ZRS is designed to provide at least `99.9999999999% (12 9's) durability of objects over a given year`. ZRS can protect your data from `datacenter-level failures`. ZRS is a good choice for `data that requires high durability` and `availability`.

**Geo-redundant storage (GRS)**: Geo-redundant storage maintains `six` copies of your data. `Three` copies are in the primary region in same `AZ` like LRS and `three` copies are in a secondary region hundreds of miles away from the primary region, providing the highest level of durability. GRS is designed to provide at least `99.99999999999999% (16 9's) durability of objects over a given year`. GRS is recommended for `business-critical data` that requires the `highest level of durability`. The data is available to be read only if Microsoft initiates a failover from the primary to secondary region.

- **Read-access geo-redundant storage (RA-GRS)**: Read-access geo-redundant storage is based on GRS. RA-GRS provides read access to the data in the secondary region, in addition to the same durability and high availability that GRS provides. RA-GRS is recommended for `business-critical data` that requires `read access` in the `secondary region`.

**Geo-zone-redundant storage (GZRS)**: Geo-zone-redundant storage maintains `six` copies of your data, Combining Geo and Zone redundancy. `Three` copies are in the primary region in 3 different `AZ` like ZRS and `three` copies are in a secondary region hundreds of miles away from the primary region, replicating the data 3 times in same data center like LRS. This provides the highest level of durability. GZRS is designed to provide at least `99.99999999999999% (16 9's) durability of objects over a given year`.

---

### URL Structure

- The URL structure for accessing the resources in Azure Storage is as follows:

```
https://<storage-account-name>.blob.core.windows.net/<container-name>/<blob-name>
```

- The URL structure for accessing the resources in Azure Files is as follows:

```
https://<storage-account-name>.file.core.windows.net/<share-name>/<directory-name>/<file-name>
```

- The URL structure for accessing the resources in Azure Queue Storage is as follows:

```
https://<storage-account-name>.queue.core.windows.net/<queue-name>
```

- The URL structure for accessing the resources in Azure Table Storage is as follows:

```
https://<storage-account-name>.table.core.windows.net/<table-name>
```

- You can also configure a custom domain name for your storage account. For more information, see [here](https://learn.microsoft.com/en-us/azure/api-management/configure-custom-domain?tabs=custom)

---

### Secure Access

In the Azure portal, each Azure service requires certain steps to configure the service endpoints and restrict network access. To access these settings for your storage account, you use the Firewalls and virtual networks settings.

- The `Firewalls` and `virtual` networks settings restrict access to your storage account from specific subnets on virtual networks or public IPs.

- You can configure the service to allow access to one or more `public IP` ranges.

- `Subnets` and `virtual networks` must exist in the same Azure region or region pair as your storage account.

