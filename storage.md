# Azure Storage

---

## Table of Contents

- [Pre-requisites](#pre-requisites)
- [Introduction](#introduction)
- [Azure Storage services](#azure-storage-services)
- [Storage Replication](#storage-replication)
- [URL Structure](#url-structure)
- [Secure Access](#secure-access)
- [Azure Storage Explorer](#azure-storage-explorer)
- [References and further reading](#references-and-further-reading)


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

## Azure Storage Account

- An Azure Storage account is a `unique namespace` in Azure that provides `storage services`. The storage account provides a unique namespace for your Azure Storage data that is accessible from anywhere in the world over HTTP or HTTPS. Data in your Azure storage account is durable and highly available, secure, and scalable. You can use your storage account to store and retrieve large amounts of unstructured data, such as documents, media files, backups, and logs.

- When you create a storage account, you have the option to choose the `performance tier` of the account. The performance tier determines the `replication strategy` that is used to store your data. The performance tier also determines the `access tier` that is used to store your data. The performance tier and access tier that you choose for your storage account affect the cost of storing data in your account. The performance tier and access tier that you choose also affect the availability and durability of your data. Types of performance tiers are 

    - `Standard`: General-purpose (v-1 and v-2) storage accounts that provide access to Azure Storage services such as `Blobs`, `Files`, `Queues`, and `Tables`. Standard storage accounts are backed by magnetic drives and are the most cost-effective option.
    - `Premium`: High-performance storage accounts that provide access to Azure Blob Storage, Azure Files, Azure Queues, and Azure Tables. Premium storage accounts are backed by solid-state drives (SSDs) and are suitable for I/O-intensive applications. `Premium` storage accounts are available only for `Block Blobs` and `Page Blobs`.`Premium files` billing is based on the provisioned size of the file share. The provisioned size is the maximum size that the file share can grow to, even if it is empty. The provisioned size is specified in `GiB` and is billed at the `premium file share rate`. The provisioned size is rounded up to the nearest `GiB`. The minimum provisioned size for a file share is `100 GiB`. The maximum provisioned size for a file share is `100 TiB`.
    
Types of access tiers are `Hot`, `Cool`, and `Archive`.

## Azure Storage services

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
        4. `Archive`: Optimized for storing data that is rarely accessed and stored for at least `180` days with flexible latency requirements. It is the lowest cost tier and usually ofline.
    - `Blob lifecycle management`: In the Azure portal, you create lifecycle management policy rules for your Azure storage account by specifying several settings. For each rule, you create `If - Then` block conditions to transition or expire data based on your specifications. The rule can be based on the time the blob was last modified or the time the blob was last accessed (read or write). To perform an action based on the access time, `access tracking` must be enabled. This can incur additional storage costs.`
        1. Define rules to automatically transition blobs to a cooler storage tier `if` they have not been accessed for a specified number of days.
        2. Define rules to automatically delete blobs at the end of their lifecycle.
        3. Define rules to automatically delete previous versions of blobs.
        4. Define rules to automatically set the access tier of blobs.
    - `Blob Types`: 
        1. `Block Blobs`: Optimized for streaming and storing cloud objects, and are a good choice for storing documents, media files, backups, and other large binary objects.
        2. `Append Blobs`: Optimized for append operations, making them ideal for scenarios such as `logging` data from virtual machines.
        3. `Page Blobs`: Optimized for random read-write operations, making them ideal for scenarios such as VHDs(storage disks for Azure VMs). A page blob can be up to 8 TB in size.
    - `Uploading Blobs`: You can upload blobs to Azure Storage using the `Azure portal`, `Azure Storage Explorer`, `Azure PowerShell`, `Azure CLI`, or an` Azure Storage client library`. You can also upload blobs using the Azure Storage REST API.
        1. `AzCopy`: A command-line utility that you can use to copy `blobs` or `files` to or from a storage account.
        2. `Azure Data Box Disk`: A service for transferring on-premises data to Blob Storage when large datasets or network constraints make uploading data over the wire unrealistic. You can use Azure Data Box Disk to request solid-state disks (SSDs) from Microsoft. You can copy your data to those disks and ship them back to Microsoft to be uploaded into Blob Storage.
        3. `Azure Import/Export`: Azure Import/Export service is used to securely import large amounts of data to Azure Blob storage and Azure Files by shipping disk drives to an Azure datacenter. This service can also be used to transfer data from Azure Blob storage to disk drives and ship to your on-premises sites. Data from one or more disk drives can be imported either to Azure Blob storage or Azure Files.
            - The jobs can be import or export jobs. An `import` job allows you to import data into Azure Blobs or Azure files whereas the `export` job allows data to be exported from Azure Blobs. For an import job, you ship drives containing your data. When you create an export job, you ship empty drives to an Azure datacenter. In each case, you can ship up to 10 disk drives per job.
    - `Blob Versioning`: Blob versioning is a feature of Azure Blob Storage that allows you to keep older versions of blobs when they are updated or deleted. You can use blob versioning to recover an earlier version of a blob if it is accidentally modified or deleted. `Object replication` can be used to replicate blobs between storage accounts. Before configuring object replication, you must enable `blob versioning for both storage accounts`, and you must enable the `change feed` for the source account. The `change feed` is a log of changes to blobs in a storage account. The change feed is used by object replication to replicate blobs between storage accounts.

- **Azure Files**: Managed file shares in the cloud that are accessible via the `Server Message Block (SMB) protocol` and the `Network File System (NFS) protocol`. Azure file shares can be mounted concurrently by cloud or on-premises deployments of Windows, macOS, and Linux. Azure file shares can also be cached on Windows Servers with Azure File Sync for fast access near where the data is being used.
    - `Azure file shares`: Azure Files provides shared access to files across multiple VMs. Any number of Azure virtual machines or roles can mount and access an Azure file share simultaneously. When configuring `SMB` Azure file share:
        1. `Open port 445`. Azure Files uses the SMB protocol. SMB communicates over TCP port 445. Be sure port 445 is open. Also, make sure your firewall isn't blocking TCP port 445 from the client machine.
        2. `Enable secure transfer`. The Secure transfer required setting enhances the security of your storage account by limiting requests to your storage account from secure connections only
        3. `File share snapshot`. You can create a snapshot of a file share to capture its state at that moment in time. Snapshots are read-only versions of the file share that can be accessed by users and applications.
    
    - `Azure file soft delete`: Azure Files supports soft delete for file shares. When you enable soft delete, you can recover your file share and its contents if they are accidentally deleted. Soft delete is a data protection feature that allows you to recover your data when it is erroneously deleted. When you delete a file share, the file share is moved to a soft-deleted state. You can then recover the file share and its contents within a retention period.

    - `Azure File Sync`: Azure File Sync enables you to cache several Azure Files shares on an `on-premises Windows Server` or `cloud virtual machine`. Azure File Sync is a service that enables you to centralize your organization's file shares in Azure Files, while keeping the flexibility, performance, and compatibility of an on-premises file server. Azure File Sync additionally has the ability to transform Windows Server into a quick cache of your Azure file share. To establish file sync with Azure file and on-premise server, 
        1. Deploy the `Azure File Sync agent` on the server. The Azure File Sync agent is a downloadable package that enables Windows Server to be synced with an Azure file share.
        2. Register the server with the Azure File Sync service. When you register a server with the Azure File Sync service, you establish a trust relationship between the server and the service. This trust relationship enables the server to sync with Azure file shares.
        3. Create a `sync group` and add a server endpoint to the `sync group`. The server endpoint represents a path on a registered server. The server endpoint is associated with a cloud endpoint, which represents an Azure file share. The cloud endpoint is associated with a storage account. The storage account contains the Azure file share that you want to sync with the server endpoint. After you create a sync group, `you can add multiple server endpoints` to the sync group. Each server endpoint can sync with the same cloud endpoint or with different cloud endpoints, but you must have only `one cloud endpoint`. 
        * `Cloud Tiering`: Azure File Sync cloud tiering enables you to store only the `newest` or `most recently accessed` files on your local server. Older or less frequently accessed files are tiered to Azure Files in the cloud. This feature helps you save on storage costs by keeping only the most frequently accessed data on-premises.

- **Azure Queue Storage**: A service for storing large numbers of `messages` that can be accessed from anywhere in the world via authenticated calls using `HTTP or HTTPS`. A single message can be up to `64 KB` in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.

- **Azure Table Storage**: A service that stores `structured NoSQL data` in the cloud, providing a key/attribute store with a schema-less design. Because Table Storage is schema-less `(non-relational)` it's easy to adapt your data as the needs of your application evolve. Access to Table Storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.

---

## Storage Replication/Redundancy

Azure Storage offers several types of replication, to ensure durability and high availability.  Azure Storage replication copies your data to protect from planned and unplanned events. These events range from transient hardware failures, network or power outages, massive natural disasters, and so on. The following are the types of replication available in Azure Storage:

**Locally redundant storage (LRS)**: Locally redundant storage maintains `three` copies of your data. LRS is replicated three times within a storage scale unit in a datacenter(a single`availability zone` in a region). LRS is designed to provide at least `99.999999999% (11 9's) durability of objects over a given year`. If a data center-level disaster occurs, such as fire or flooding, all replicas might be lost or unrecoverable. Despite its limitations, LRS can be appropriate in several scenarios. This can be good for `constantly changing data` , `non-critical data` that can be easily restored , region/zone data `restrictions`.

**Zone-redundant storage (ZRS)**: Zone-redundant storage maintains `three` copies of your data across three storage clusters(3 availability zones) in a single region.  `Each storage cluster is physically separated from the others and resides in its own availability zone providing higher durability than LRS. ZRS is designed to provide at least `99.9999999999% (12 9's) durability of objects over a given year`. ZRS can protect your data from `datacenter-level failures`. ZRS is a good choice for `data that requires high durability` and `availability`.

**Geo-redundant storage (GRS)**: Geo-redundant storage maintains `six` copies of your data. `Three` copies are in the primary region in same `AZ` like LRS and `three` copies are in a secondary region hundreds of miles away from the primary region, providing the highest level of durability. GRS is designed to provide at least `99.99999999999999% (16 9's) durability of objects over a given year`. GRS is recommended for `business-critical data` that requires the `highest level of durability`. The data is available to be read only if Microsoft initiates a failover from the primary to secondary region.

- **Read-access geo-redundant storage (RA-GRS)**: Normally, you can read data from the primary region but not from the secondary region. Read-access geo-redundant storage is based on GRS. RA-GRS provides read access to the data in the secondary region, in addition to the same durability and high availability that GRS provides. RA-GRS is recommended for `business-critical data` that requires `read access` in the `secondary region`.

**Geo-zone-redundant storage (GZRS)**: Geo-zone-redundant storage maintains `six` copies of your data, Combining Geo and Zone redundancy. `Three` copies are in the primary region in 3 different `AZ` like ZRS and `three` copies are in a secondary region hundreds of miles away from the primary region, replicating the data 3 times in same data center like LRS. This provides the highest level of durability. GZRS is designed to provide at least `99.99999999999999% (16 9's) durability of objects over a given year`.

---

## URL Structure

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

## Secure Access

With encryption, authentication, authorization, and user access control with credentials, file permissions, and private signatures, Azure Storage helps you secure your data for compliance needs. Azure Storage provides several security features to help you protect your data:

- **Shared Access Signature (SAS)**: A shared access signature (SAS) provides secure delegated access to resources in your storage account. With a SAS, you can grant limited permissions to clients who should not have the account key but should be able to perform certain operations. A SAS is a token that encapsulates a set of permissions for a resource and specifies how the resource may be accessed. Access keys provide full control over the resources in your storage account. By using a SAS, you can grant limited access to your storage account to clients who should not have the account `access keys`.
    - You can provide a SAS to clients who should not have the account key but who should be able to access a resource. By distributing a SAS URI to clients, you can grant them access to a resource for a specified period of time. 
    - You can also revoke access by changing the SAS. 
    - A SAS can be scoped to a container, a blob, a table, a queue, or a file share. 
    - You can also specify the permissions that are granted to the client, such as read, write, or delete. 
    - You can also specify the IP addresses from which the SAS can be used. 
    - You can also specify the protocol that the client must use to access the resource. 
    - You can also specify the start and expiry times for the SAS. 
    - Configuring a SAS is a two-step process. First, you create a stored access policy on a resource. Then, you generate a SAS that references that stored access policy:
        - `Signing method`: Choose the signing method: Account key or User delegation key.
        - `Signing key`: Select the signing key from your list of keys.
        - `Permissions`: Select the permissions granted by the SAS, such as read or write.
        - `Start and Expiry date/time`: Specify the time interval for which the SAS is valid. Set the start time and the expiry time.
        - `Allowed IP addresses`: (Optional) Identify an IP address or range of IP addresses from which Azure Storage accepts the SAS.
        - `Allowed protocols`: (Optional) Select the protocol over which Azure Storage accepts the SAS.
    - `SAS Types`: 
        1. `Service SAS`: Grants access to a resource in one of the storage services: Blob, Queue, Table, or File. Use a service SAS when you want to give access to a resource in one of the storage services, but not the account itself.
        2. `Account SAS`: Grants access to resources in one or more of the storage services. Use an account SAS when you want to give access to resources in one or more of the storage services, but not the account itself.
    - `SAS URI`: A SAS URI is a URI that includes a SAS token. You can use a SAS URI to grant access to a resource for a specified period of time. You can also revoke access by changing the SAS. The URI can contains the SAS token, which includes the permissions granted by the SAS, the start and expiry times for the SAS, and the signature that was used to create the SAS. Sample SAS URI:
        ```
        https://<storage-account-name>.blob.core.windows.net/<container-name>/<blob-name>?<SAS-token>
        ```

- **Encryption**: Azure Storage encrypts your data at rest by default when you use Azure Storage encryption. 
    - Azure Storage encryption is enabled for all storage accounts, including Blob Storage, File Storage, Queue Storage, and Table Storage. 
    - Azure Storage encryption is transparent to you, the developer. 
    - Azure Storage handles all encryption, decryption, and key management in a fully transparent fashion.
    - In the Azure portal, you configure Azure Storage encryption by specifying the encryption type. 
    - You can manage the keys yourself, or you can have the keys managed by Microsoft.
    - `Customer-managed keys`: You can use your own keys to encrypt and decrypt your data. You can also use Azure Key Vault to manage your keys.
  
- **Configure service endpoints**: In the Azure portal, each Azure service requires certain steps to configure the service endpoints and restrict network access. To access these settings for your storage account, you use the Firewalls and virtual networks settings.

    - The `Firewalls` and `virtual` networks settings restrict access to your storage account from specific subnets on virtual networks or public IPs.

    - You can configure the service to allow access to one or more `public IP` ranges.

    - `Subnets` and `virtual networks` must exist in the same Azure region or region pair as your storage account.

---

## Azure Storage Explorer

Azure Storage Explorer is a standalone application that makes it easy to work with Azure Storage data on Windows, macOS, and Linux. With Azure Storage Explorer, you can access multiple accounts and subscriptions, and manage all your storage content.

#### Things to Know About Azure Storage Explorer
- Azure Storage Explorer requires both management (Azure Resource Manager) and data layer permissions to allow full access to your resources. You need Azure Active Directory (Azure AD) permissions to access your storage account, the containers in your account, and the data in the containers.
- Azure Storage Explorer lets you connect to different storage accounts.
    - Connect to storage accounts associated with your Azure subscriptions.
    - Connect to storage accounts and services that are shared from other Azure subscriptions.
    - Connect to and manage local storage by using the Azure Storage Emulator.

#### Scenarios Supported by Azure Storage Explorer
Azure Storage Explorer supports various scenarios for working with storage accounts in global and national Azure. Here are some common scenarios:

| **Scenario** | **Description** |
| ------------ | ---------------- |
| Connect to an Azure subscription | Manage storage resources that belong to your Azure subscription. |
| Work with local development storage | Manage local storage by using the Azure Storage Emulator. |
| Attach to external storage | Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account name, key, and endpoints. |
| Attach a storage account with a SAS | Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS). |
| Attach a service with a SAS | Manage a specific Azure Storage service (blob container, queue, or table) that belongs to another Azure subscription by using a SAS. |

#### Attach to External Storage Account
Azure Storage Explorer allows you to attach to external storage accounts for easy sharing of storage resources. To create the connection, you need the external storage account name and account key. In the Azure portal, the account key is called key1.

**Access Keys:**
- Access keys provide access to the entire storage account. You're provided two access keys so you can maintain connections by using one key while regenerating the other.
- **Important:** Store your access keys securely. We recommend regenerating your access keys regularly. When you regenerate your access keys, you must update any Azure resources and applications that access this storage account to use the new keys. This action doesn't interrupt access to disks from your virtual machines.

---

# References and further reading

- [Azure Storage Documentation](https://docs.microsoft.com/en-us/azure/storage/)
- [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/)
