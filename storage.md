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

**Azure Blob Storage**: Store and manage unstructured data. Blobs can be text or binary files, such as documents, media files, and application installers. They can also store data for backup, restore, disaster recovery, and archiving. Objects in Blob Storage can be accessed from anywhere in the world via `HTTP or HTTPS`. Users or client applications can access blobs via `URLs`, the Azure Storage REST API, Azure PowerShell, the Azure CLI, or an Azure Storage client library. The storage client libraries are available for multiple languages, including .NET, Java, Node.js, Python, PHP, and Ruby.

**Azure Files**: Managed file shares in the cloud that are accessible via the `Server Message Block (SMB) protocol` and the `Network File System (NFS) protocol`. Azure file shares can be mounted concurrently by cloud or on-premises deployments of Windows, macOS, and Linux. Azure file shares can also be cached on Windows Servers with Azure File Sync for fast access near where the data is being used.

**Azure Queue Storage**: A service for storing large numbers of `messages` that can be accessed from anywhere in the world via authenticated calls using `HTTP or HTTPS`. A single message can be up to `64 KB` in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.

**Azure Table Storage**: A service that stores `structured NoSQL data` in the cloud, providing a key/attribute store with a schema-less design. Because Table Storage is schema-less `(non-relational)` it's easy to adapt your data as the needs of your application evolve. Access to Table Storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.

---

### Storage Replication

Azure Storage offers several types of replication, to ensure durability and high availability.  Azure Storage replication copies your data to protect from planned and unplanned events. These events range from transient hardware failures, network or power outages, massive natural disasters, and so on. The following are the types of replication available in Azure Storage:

**Locally redundant storage (LRS)**: Locally redundant storage maintains `three` copies of your data. LRS is replicated three times within a storage scale unit in a datacenter(a single`availability zone` in a region). LRS is designed to provide at least `99.999999999% (11 9's) durability of objects over a given year`. If a data center-level disaster occurs, such as fire or flooding, all replicas might be lost or unrecoverable. Despite its limitations, LRS can be appropriate in several scenarios. This can be good for `constantly changing data` , `non-critical data` that can be easily restored , region/zone data `restrictions`.

**Zone-redundant storage (ZRS)**: Zone-redundant storage maintains `three` copies of your data across three storage clusters(3 availability zones) in a single region.  `Each storage cluster is physically separated from the others and resides in its own availability zone providing higher durability than LRS. ZRS is designed to provide at least `99.9999999999% (12 9's) durability of objects over a given year`. ZRS can protect your data from `datacenter-level failures`. ZRS is a good choice for `data that requires high durability` and `availability`.

**Geo-redundant storage (GRS)**: Geo-redundant storage maintains `six` copies of your data. `Three` copies are in the primary region in same `AZ` like LRS and `three` copies are in a secondary region hundreds of miles away from the primary region, providing the highest level of durability. GRS is designed to provide at least `99.99999999999999% (16 9's) durability of objects over a given year`. GRS is recommended for `business-critical data` that requires the `highest level of durability`. The data is available to be read only if Microsoft initiates a failover from the primary to secondary region.

- **Read-access geo-redundant storage (RA-GRS)**: Read-access geo-redundant storage is based on GRS. RA-GRS provides read access to the data in the secondary region, in addition to the same durability and high availability that GRS provides. RA-GRS is recommended for `business-critical data` that requires `read access` in the `secondary region`.

**Geo-zone-redundant storage (GZRS)**: Geo-zone-redundant storage maintains `six` copies of your data, Combining Geo and Zone redundancy. `Three` copies are in the primary region in 3 different `AZ` like ZRS and `three` copies are in a secondary region hundreds of miles away from the primary region, replicating the data 3 times in same data center like LRS. This provides the highest level of durability. GZRS is designed to provide at least `99.99999999999999% (16 9's) durability of objects over a given year`.

---