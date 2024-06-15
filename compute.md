# Azure Compute

## Pre-requisites

- Understanding of Azure fundamentals, Familiarity with Infrastructure as a Service (IaaS), virtualization, Azure subscriptions, resource groups, networking, storage.
- Azure portal. Ability to create and configure resources in the Azure portal.
- An Azure account with an active subscription (Free tier is enough). Sign up or login to your Azure account [here](https://azure.microsoft.com/en-us/free/)    

## Overview

Azure Compute is an on-demand computing service for running cloud-based applications. It provides computing resources such as virtual machines (`providing its own operating system, storage, and networking capabilities, and can run a wide range of applications.`), containers, serverless computing, and batch processing. Azure Compute allows you to scale resources up or down based on demand, pay only for the resources you use, and deploy applications across multiple regions for high availability.

## Virtual Machines

Azure Virtual Machines (VMs) are on-demand, scalable computing resources provided by Azure. They are similar to physical computers but run on a shared physical hardware. Azure VMs can be used to run applications, host websites, and perform various computing tasks. You can choose from a wide range of VM sizes and configurations based on your requirements. Azure VMs can be created and managed through the Azure portal, Azure CLI, PowerShell, and other tools. To create a VM, you need to specify:

- **VM name**: The virtual machine name is used as the computer name, which is configured as part of the operating system. You can specify a name with up to 15 characters on a Windows virtual machine and 64 characters on a Linux virtual machine. VM names should be consistent with the naming conventions of your organization. Eg. `devusc-webvm01` - `dev` stands for development and`usc` identifies the location. `web` indicates the machine as a web server, and the suffix 01 shows the machine is the first instance in the configuration.

- **VM location**: The Azure region where the virtual machine will be deployed. You should choose a location that is geographically close to your users to reduce latency and improve performance. Also consider there are price difference and hardware availability between regions.

- **VM size**: The size of the virtual machine determines the number of CPU cores, memory, and disk space available. You can choose from a wide range of VM sizes based on your requirements. The size of the VM can be changed later if needed. This table provides a description of different Azure virtual machine (VM) classifications, along with typical scenarios for their use.

| **Classification**     | **Description**                                                                                       | **Scenarios**                                                                                          |
|-------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **General Purpose**     | General-purpose virtual machines are designed to have a balanced CPU-to-memory ratio.                 | - Testing and development<br>- Small to medium databases<br>- Low to medium traffic web servers         |
| **Compute Optimized**   | Compute optimized virtual machines are designed to have a high CPU-to-memory ratio.                   | - Medium traffic web servers<br>- Network appliances<br>- Batch processes<br>- Application servers       |
| **Memory Optimized**    | Memory optimized virtual machines are designed to have a high memory-to-CPU ratio.                    | - Relational database servers<br>- Medium to large caches<br>- In-memory analytics                       |
| **Storage Optimized**   | Storage optimized virtual machines are designed to have high disk throughput and I/O.                 | - Big Data<br>- SQL and NoSQL databases<br>- Data warehousing<br>- Large transactional databases         |
| **GPU**                 | GPU virtual machines are specialized virtual machines targeted for heavy graphics rendering and video editing. Available with single or multiple GPUs. | - Model training<br>- Inferencing with deep learning                                                     |
| **High Performance Compute** | High performance compute offers the fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA). | - Workloads that require fast performance<br>- High traffic networks                                      |



- **Networking**: The virtual network and subnet where the virtual machine will be deployed. You can configure network security groups, public IP addresses, and other networking settings.

- **Storage**: The storage account and disk type for the virtual machine. You can choose between standard HDD, standard SSD, and premium SSD disks based on your performance requirements. There are atleast 2 types of disks that can be attached to a VM:
    * **OS disk**: The disk that contains the operating system and boot files. It is required for the virtual machine to start and run.
    * **Data disk**: Additional disks that can be attached to the virtual machine for storing data. Data disks can be used for applications, databases, or other storage needs.

- **Operating system**: The operating system image that will be used to create the virtual machine. You can choose from a variety of `Windows` and `Linux images` available in the Azure Marketplace. Other images can include popular software tools such as SQL Server, SharePoint, and more. Optionally, you can bring your own custom image.

- **Pricing**: A subscription is billed two separate costs for every virtual machine: `compute and storage`. By separating these costs, you can scale them independently and only pay for what you need.
    * **Compute expenses**: are priced on a `per-hour` basis but billed on a `per-minute` basis. If the virtual machine is deployed for 55 minutes, you're charged for only 55 minutes of usage. With the `consumption-based` option, you pay for compute capacity by the second. You're able to increase or decrease compute capacity on demand and start or stop at any time. With the `reserved instances` option, you can save money by committing to a one- or three-year term for a discount on the compute resources.
    * **Storage expenses**: are billed separately from compute resources. You pay for the storage capacity you use, and the number of transactions performed on that storage. The storage costs are based on the type of storage you use, such as standard HDD, standard SSD, or premium SSD.

### Steps to Create a Virtual Machine

1. **Navigate to the Azure portal**: [Azure Portal](https://portal.azure.com/).
2. **Click on `Create a resource`**: In the Azure portal, click on the `Create a resource` button in the upper left corner.
3. **Search for `Virtual Machine`**: In the search bar, type `Virtual Machine` and press Enter.
4. **Select `Virtual Machine`**: From the search results, select `Virtual Machine` and click on the `Create` button.
5. **Configure**:  configuring basic and advanced options, and specifying details about the disks, virtual networks, and machine management:
    - **Basics**: The Basics tab contains the project details, administrator account, and inbound port rules.
    - **Disks**: On the Disks tab, you select the OS disk type and specify your data disks.
    - **Networking**: The Networking tab provides settings to create virtual networks and load balancing.
    - **Management**: On the Management tab, you can enable auto-shutdown and specify backup details.
    - **Advanced**: On the Advanced tab, you can configure agents, scripts, or virtual machine extensions.
    - Other settings are available on the Monitoring and Tags tabs.

- Alternatively, you can browse to the [Azure Quickstart Templates](https://learn.microsoft.com/en-us/samples/browse/?expanded=azure&products=azure-resource-manager) page to find pre-configured templates for virtual machines. You can select a template, customize it, and deploy it directly from the Azure portal.

### Connecting to a Virtual Machine

Once the virtual machine is created, you can connect to it using various methods:

- **SSH (Secure Shell)**: For Linux virtual machines, you can use SSH to connect to the VM. You need the public IP address or DNS name of the VM, and the SSH private key.

- **RDP (Remote Desktop Protocol)**: For Windows virtual machines, you can use RDP to connect to the VM. You need the public IP address or DNS name of the VM, and the username and password you specified during VM creation. The system provides you with a downloadable RDP file to use for the connection.

- **Azure Bastion**: Azure Bastion is a fully managed PaaS service that provides secure and seamless `RDP and SSH` access to your virtual machines directly through the Azure portal directly over SSL. It eliminates the need for a public IP address on the virtual machine. Azure Bastion lets you connect to the virtual machine directly from the Azure portal. You aren't a client, agent, or another piece of software.

- **Azure Serial Console**: Azure Serial Console provides access to the serial console of your virtual machine. It can be used to troubleshoot boot issues, network configuration problems, and other system-related issues.

### Managing Virtual Machines

Once the virtual machine is created, you can manage it using the Azure portal, Azure CLI, PowerShell, or other tools. Some common management tasks include:

- **Start/Stop**: You can start, stop, restart, or deallocate a virtual machine based on your requirements. Stopping a VM deallocates the compute resources and stops billing for the VM. Deallocating a VM releases the compute resources and the public IP address.

- **Resize**: You can resize a virtual machine to change the VM size, CPU cores, memory, and disk space. You can scale up or down based on your requirements.

- **Backup**: You can configure backup policies to protect your virtual machine data. Azure Backup provides backup and restore capabilities for virtual machines.

- **Monitoring**: You can monitor the performance and health of your virtual machine using Azure Monitor. You can set up alerts, view metrics, and analyze performance data. Azure platform monitors and predicts that the hardware or any platform component associated to a physical machine is about to fail. Azure uses `Live Migration` technology to migrate`(heal)` your virtual machines from the failing hardware to a healthy physical machine. Live Migration is a virtual machine preserving operation that only pauses the virtual machine for a short time, but performance might be reduced before or after the event.

- **Security**: You can configure security settings, network security groups, and encryption for your virtual machine. You can also enable Azure Security Center for advanced threat protection.

- **Automation**: You can automate management tasks using Azure Automation, Azure Functions, or other automation tools. You can create runbooks, scripts, and workflows to streamline operations.

- **Scaling**: You can scale virtual machines manually or automatically based on demand. You can use Azure Autoscale to automatically adjust the number of VM instances based on predefined rules.

- **High Availability**: You can configure availability sets, availability zones, or virtual machine scale sets for high availability and fault tolerance. You can distribute VM instances across multiple fault domains and update domains to ensure uptime. 


## Virtual Machine Scale Sets

Azure Virtual Machine Scale Sets are an Azure compute resource that you can use to deploy and manage a set of identical VMs. With VM scale sets, you can create and manage a group of load-balanced VMs that can automatically scale in and out based on demand or a defined schedule. VM scale sets are designed for high availability and fault tolerance, and they can be used to run large-scale services such as web front ends, containerized workloads, and microservices. Virtual Machine Scale Sets support up to `1,000` virtual machine instances. If you create and upload your own `custom virtual machine images, the limit is 600` virtual machine instances.


### Availability Sets vs. Availability Zones

- **Availability Sets**: An availability set is a logical feature you can use to ensure `a group of related virtual machines are deployed together`. The grouping helps to prevent a single point of failure from affecting all of your machines. The grouping ensures that not all of the machines are upgraded at the same time during a host operating system upgrade in the datacenter. Azure ensures that virtual machines in an availability set run across multiple physical servers, compute racks, storage units, and network switches. If a hardware or software failure occurs, only a subset of your VMs are impacted and your overall solution remains available and operational. Availability sets are used for high availability and fault tolerance.

    * **Fault Domain**: A fault domain is a group of virtual machines that share a common power source and network switch. By default, the VMs in an availability set are separated across up to three fault domains for Resource Manager deployments (two fault domains for classic deployments). This configuration ensures that the VMs are isolated from each other when it comes to power and networking.

    * **Update Domain**: An update domain is a group of virtual machines that can be rebooted at the same time. When more than one update domain is configured, the virtual machines in one update domain are rebooted while the virtual machines in the other update domains remain running. This configuration ensures that the VMs are isolated from each other when it comes to planned maintenance events. By default, five update domains are assigned to the VMs in an availability set and can be increased to a maximum of 20.

- **Availability Zones**: Availability Zones are unique physical locations within an Azure region. Each zone is made up of one or more datacenters equipped with independent power, cooling, and networking. Availability Zones allow you to run mission-critical applications with high availability and low-latency replication. If one zone is compromised, the other zones are unaffected. By using Availability Zones, you can protect your applications and data from datacenter failures. Availability Zones are used for high availability and disaster recovery. `Zone-redundant services` replicate your applications and data across availability zones to protect against single-points-of-failure.

- **Auto-Scaling**: Virtual Machine Scale Sets can automatically increase or decrease the number of VM instances based on demand. You can configure autoscale settings to define scaling rules based on metrics such as CPU utilization, memory usage, or network traffic. Autoscaling helps to optimize resource utilization and reduce costs by scaling out during peak demand and scaling in during off-peak hours. You can also define a schedule-based scaling rule to scale the VM instances based on a predefined schedule.

### Vertical vs. Horizontal Scaling

- **Vertical Scaling**: Vertical scaling, also known as `scaling up`, involves increasing the size of a single virtual machine. You can add more CPU cores, memory, or disk space to the VM to handle increased workloads. Vertical scaling is useful when you need to increase the capacity of a single VM to meet performance requirements. However, there is a limit to how much you can scale a single VM vertically.

- **Horizontal Scaling**: Horizontal scaling, also known as `scaling out`, involves adding more virtual machines to distribute the workload. You can create a group of identical VMs using VM scale sets and distribute the load across the VM instances. Horizontal scaling is useful when you need to handle increased traffic or demand by adding more VM instances. Horizontal scaling provides better fault tolerance and high availability compared to vertical scaling.


### Steps to Create a Virtual Machine Scale Set

1. **Navigate to the Azure portal**: [Azure Portal](https://portal.azure.com/).

2. **Click on `Create a resource`**: In the Azure portal, click on the `Create a resource` button in the upper left corner.

3. **Search for `Virtual Machine Scale Set`**: In the search bar, type `Virtual Machine Scale Set` and press Enter.

4. **Select `Virtual Machine Scale Set`**: From the search results, select `Virtual Machine Scale Set` and click on the `Create` button.

5. **Configure**:  configuring basic and advanced options, and specifying details about the disks, virtual networks, and machine management:
    - **Basics**: The Basics tab contains the project details, administrator account, and inbound port rules:
        - **Ochestration mode**: Choose how virtual machines are managed by the scale set. In `flexible orchestration mode`, you manually create and add a virtual machine of any configuration to the scale set. In `uniform orchestration mode`, you define a virtual machine model and Azure will generate identical instances based on that model.
        - **Image**: Select the operating system image that will be used to create the virtual machine scale set. You can choose from a variety of Windows and Linux images available in the Azure Marketplace.
        - **Size**: Choose the size of the virtual machines in the scale set. You can select from a range of VM sizes based on your requirements.
        - **Run with Azure Spot Discount**: Azure Spot Instances allow you to take advantage of unused Azure capacity at a discounted price. Spot Instances can be evicted if Azure needs the capacity back, but they can be a cost-effective option for certain workloads.
    - **Disks**: On the Disks tab, you select the OS disk type and specify your data disks.
    - **Networking**: The Networking tab provides settings to create virtual networks and load balancing.
    - **Management**: On the Management tab, you can enable auto-shutdown and specify backup details.
    - **Scaling**: On the Scaling tab, you can configure autoscale settings and define scaling rules.
        - **Scaling policy**: Choose the scaling policy for the scale set. You can define scaling rules based on metrics such as CPU utilization, memory usage, or network traffic. Define the minimum and maximum number of VM instances.
        - **Scale out**: Define the conditions under which the scale set should increase the number of VM instances. `CPU Threshold` to trigger scale out, `Duration in minutes` to observe for metrics and sustain the condition before scaling out again, and `Number of instances to increase by`.
        - **Scale in**: Define the conditions under which the scale set should decrease the number of VM instances. `CPU Threshold` to trigger scale in, `Duration in minutes` to observe for metrics and sustain the condition before scaling in again, and `Number of instances to decrease by`.
    - **Health probes**: On the Health probes tab, you can configure health probes for load balancing.
    - **Other settings**: Other settings are available on the Monitoring, Tags, and Advanced tabs.
    - **Advanced**: On the Advanced tab, you can configure `Enable scaling beyond 100 instances` and `Spreading algorithm`.


## App Service

Azure App Service is a fully managed platform for building, deploying, and scaling web apps and APIs. It provides a rich set of features for building and hosting web applications, mobile backends, and RESTful APIs. Azure App Service supports multiple programming languages, frameworks, and tools, including .NET, Java, Node.js, PHP, Python, and Ruby. You can deploy web apps and APIs to Azure App Service using various deployment methods, such as Git, GitHub, Azure DevOps, and Docker containers. Azure App Service provides built-in DevOps capabilities for continuous integration and continuous deployment (CI/CD), automatic scaling, and monitoring.

**App Service Plans**:
- **Shared**: The Shared plan is a multi-tenant hosting plan that provides basic features for small-scale web apps. It is suitable for development and testing scenarios.
- **Basic**: The Basic plan provides dedicated virtual machine instances for web apps. It offers more resources and features than the Shared plan and is suitable for production workloads.
- **Standard**: The Standard plan provides additional features such as custom domains, SSL certificates, and auto-scaling. It is suitable for production workloads that require high availability and scalability.
- **Premium**: The Premium plan offers advanced features such as virtual network integration, custom domains with SSL, and auto-scaling. It is suitable for mission-critical workloads that require high performance and security.
- **Isolated**: The Isolated plan provides dedicated virtual machines and network isolation for web apps. It offers advanced features such as virtual network integration, custom domains with SSL, and auto-scaling. It is suitable for workloads that require high performance, security, and compliance.

**App Service scaling options**:
- **scale up**: Scale up increases the size of the VM instances that run your app, like Vertical Scaling.
- **scale out**: Increase the number of VM instances that run your app. This is Horizontal Scaling.
- **metric-based autoscale**: Automatically adjust the number of VM instances based on a specified metric, such as CPU utilization or memory usage.
- **time-based autoscale**: Automatically adjust the number of VM instances based on a predefined schedule.

**App Service Deployment Options**:
- **Local Git**: Deploy your app by pushing the code to a Git repository hosted on Azure App Service.
- **GitHub**: Deploy your app by connecting to a GitHub repository.
- **Azure DevOps**: Deploy your app using Azure DevOps pipelines.
- **Visual Studio**: Deploy your app directly from Visual Studio using the Azure App Service extension.

**Deployment Slots**:
- Deployment slots are live apps with their own hostnames. You can deploy different versions of your app to different slots and swap between them to test changes in production. Deployment slots are useful for staging, testing, and production environments. This can ensure `reductionin downtime`, `restoring to last known good site` and `Auto swap`(to swap between staging and production slots). Deployment slots are available in the `Standard, Premium, and Isolated App Service pricing tiers`.
- When you clone a configuration from another deployment slot, the cloned configuration is editable. Some configuration elements follow the content across the swap, but some don't. For example, if you clone a configuration from a slot, the `connection strings`, `Hybrid connections`,`Service endpoints`, `Azure Content Delivery Network` and `app settings`, etc are cloned. Other slot-specific configuration elements stay in the source slot after the swap.

**App Service and DNS**:
- Azure App Service provides a default domain name for your app, such as `https://<app-name>.azurewebsites.net`. You can also configure a custom domain name for your app using Azure DNS or a third-party DNS provider. You can map your custom domain to the default domain using a CNAME record or an A record. Azure App Service provides built-in support for SSL certificates and HTTPS. You can configure SSL certificates for your custom domain to secure your app.

**App Service Backup and Restore**:
- Azure App Service provides built-in backup and restore capabilities for web apps. You can configure backup policies to protect your app data and restore it in case of data loss. To use the Backup and Restore feature, you need the Standard or Premium tier App Service plan for your app or site. 
- Azure backs up `App configuration settings`, `File content`, `Any database connected to your app (SQL Database, Azure Database for MySQL, Azure Database for PostgreSQL, MySQL in-app)`.
- In your storage account and container configured for your app, each backup consists of a `Zip` file and `XML file:
    * The Zip file contains the back-up data for your app or site.
    * The XML file contains a manifest of the Zip file contents.
    * Backups can hold up to 10 GB of app and database content.
    * If your storage account is enabled with a firewall, you can't use the storage account as the destination for your backups.

**App Service Monitoring**:
- Azure App Service provides built-in monitoring and diagnostics capabilities for web apps. You can view metrics, logs, and alerts to monitor the performance and health of your app. Azure Monitor provides a centralized platform for monitoring and analyzing data from your app. You can set up alerts based on metrics such as CPU utilization, memory usage, and response time. `Azure Application Insights` provides advanced monitoring capabilities for web apps, including performance monitoring, error tracking, and user analytics.

### Azure Container Instances

Containerization is a lightweight, portable, and scalable way to run applications. Containers package an application and its dependencies into a single `image` that can be run on any platform. Azure Container Instances (ACI) is a serverless container service that allows you to run containers without managing the underlying infrastructure. ACI provides a fast and easy way to deploy containers in the cloud. You can run containers on-demand, scale containers based on demand, and pay only for the resources you use. ACI supports both Linux and Windows containers and integrates with other Azure services such as Azure Container Registry and Azure Kubernetes Service.

**Container Groups**:
- A container group is a collection of containers that are scheduled to run on the same host machine. A container group is similar to a pod in Kubernetes. You can define a container group with one or more containers that share the same lifecycle, networking, and storage. Container groups are useful for running multi-container applications that need to be deployed together. They are useful when you want to divide a single functional task into a few container images. The images can be delivered by different teams and have separate resource requirements.
- There are two common ways to deploy a multi-container group: `Azure Resource Manager (ARM) templates`(recommended when deploying withother resources) and `YAML files`(recommended for deploying only container instances).
- Container groups can be deployed in a virtual network for secure communication between containers.
- Consider the following scenarios for working with multi-container groups:
    * **Microservices**: Deploying a set of microservices that work together to provide a complete application.
    * **front-end and back-end support**: Deploying a front-end web application and a back-end API that communicate with each other.
    * **log data collection**: Deploying a container that collects log data from other containers in the group.

**Azure Container Registry**:
- Azure Container Registry is a managed Docker registry service that allows you to store and manage container images. You can use Azure Container Registry to build, store, and deploy container images to Azure services such as Azure Container Instances and Azure Kubernetes Service. Azure Container Registry provides a secure and private registry for your container images. You can control access to your container images using Azure Active Directory and role-based access control (RBAC). Azure Container Registry integrates with Azure DevOps for continuous integration and continuous deployment (CI/CD) pipelines.

**Container Management Solutions**: The two main container management solutions in Azure are `Azure Kubernetes Service (AKS)` and `Azure Container Apps (ACA)`. Both services provide container orchestration and management capabilities, but they are designed for different use cases.

| **Feature**    | **Azure Container Apps (ACA)**                                                                                         | **Azure Kubernetes Service (AKS)**                                                                                              |
|----------------|------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **Overview**   | ACA is a serverless container platform that simplifies the deployment and management of microservices-based applications by abstracting away the underlying infrastructure. | AKS simplifies deploying a managed Kubernetes cluster in Azure by offloading the operational overhead to Azure. It’s suitable for complex applications that require orchestration. |
| **Deployment** | ACA provides a PaaS experience with quick deployment and management capabilities.                                       | AKS offers more control and customization options for Kubernetes environments, making it suitable for complex applications and microservices. |
| **Management** | ACA builds upon AKS and offers a simplified PaaS experience for running containers, with additional features like Dapr for microservices. | AKS provides a more granular control over the Kubernetes environment, suitable for teams with Kubernetes expertise.            |
| **Scalability**| ACA supports both HTTP-based autoscaling and event-driven scaling, making it ideal for applications that need to respond quickly to changes in demand. | AKS offers horizontal pod autoscaling and cluster autoscaling, providing robust scalability options for containerized applications. |
| **Use Cases**  | ACA is designed for microservices and serverless applications that benefit from rapid scaling and simplified management. | AKS is best for complex, long-running applications that require full Kubernetes features and tight integration with other Azure services. |
| **Integration**| ACA integrates with Azure Logic Apps, Functions, and Event Grid for event-driven architectures.                        | AKS provides features like Azure Policy for Kubernetes, Azure Monitor for containers, and Azure Defender for Kubernetes for comprehensive security and governance. |


## Azure Backup

* Azure Backup is a cloud-based backup service that allows you to protect your data and applications in the cloud. Azure Backup provides a simple and cost-effective solution for backing up and restoring data in Azure. You can use Azure Backup to protect virtual machines, databases, files, and folders in Azure. Azure Backup provides built-in features for data retention, encryption, and monitoring. You can configure backup policies to protect your data and restore it in case of data loss. Azure Backup integrates with other Azure services such as Azure Virtual Machines, Azure SQL Database, and Azure Blob Storage. Azure backup helps with `Compliance` and `Monitoring`.

* Azure Backup stores backed-up data in vaults: `Recovery Services vaults` and `Backup vaults`. A vault is an online-storage entity in Azure that's used to hold data such as backup copies, recovery points, and backup policies.

* **Backups can be**:
    - **Full**: A full backup is a complete copy of the data that you want to protect. Full backups are typically performed periodically to capture all the data. At most once per day.
    - **Incremental`/`Diferential**: An incremental backup captures only the changes made since the last backup. Incremental backups are performed more frequently than full backups to reduce the amount of data that needs to be backed up. At most once per day. You can't configure a `full backup` and a `differential backup` on the same day.
    - **Log backup**: A log backup captures the transaction log changes made to a database since the last log backup. Log backups are used to restore a database to a specific point in time up to a particular second. Log backups are performed frequently to capture all the changes made to the database. At most once per 15 minutes.

* **Backup Extensions**:
    - This is the first step to every back-up. Integration with the actual workload (such as Azure VM or Azure Blobs) happens at this layer. A backup extension specific to each workload is installed on the source VM or a worker VM. At the time of backup (as defined by the user in the Backup Policy), the backup extension generates the backup, which could be a snapshot, a copy of the data, or a log backup. The backup extension is responsible for ensuring that the backup is consistent and application-aware. The backup extension is also responsible for ensuring that the backup is encrypted and compressed before it is sent to the vault.

* **Backup `Access` tier**:
    - **Snapshot**: These are the quickest restores because they eliminate the wait time for snapshots to get copied to from the vault. The snapshot taken is stored along with the disk. The snapshots of the VM/Azure Files/Azure Blobs/and so on, are retained in the customer’s subscription itself in a specified resource group, and available locally to the customer.
    - **Vault-standard tier**: Backup data for all workloads supported by Azure Backup is stored in vaults, which hold backup storage, an autoscaling set of storage accounts managed by Azure Backup. The Vault-Standard tier is an online storage tier that allows you to store an isolated copy of backup data in a Microsoft-managed tenant, thus creating an extra layer of protection. For workloads where snapshot tier is supported, there's a copy of the backup data in both the snapshot tier and the vault-standard tier. The vault-standard tier ensures that backup data is available even if the data source being backed up is deleted or compromised.
    - **Archive Tier**: The Archive tier is a storage tier that allows you to store backup data in a cost-effective manner. The Archive tier is designed for long-term retention of backup data that is rarely accessed. TCustomers rely on Azure Backup for storing backup data, including their Long-Term Retention (LTR) backup data with retention needs being defined by the organization's compliance rules. In most cases, the older backup data is rarely accessed and is only stored for compliance needs.

* **Availability and Security**: 
    - The backup data is replicated across zones or regions (based on the redundancy specified by the user). You can choose from `locally redundant storage (LRS)`, `Geo-redundant storage (GRS)`, or `zone-redundant storage (ZRS)`. These options provide you with highly available data storage capabilities.
    - The data is kept safe by `encrypting` it and implementing `role-based access control (RBAC)`. You choose who can perform backup and restore operations. Azure Backup also provides protection against malicious deletion of your backup by using `soft-delete operations`. A deleted backup is stored for 14 days, free of charge, which allows you to recover the backup if needed.

* **Management**:
    - Azure Backup provides a centralized platform for managing backup policies - **`Backup Center`** on the azure portal, monitoring backup jobs, and restoring data. You can configure backup policies to protect your data and define retention rules for backup data. You can monitor backup jobs, view backup reports, and set up alerts based on backup status. Azure Backup provides built-in support for data encryption, compression, and deduplication to optimize storage usage and reduce costs.

### Virtual Machine Backup

There are four options for backing up Azure VMs:

- **Azure Backup**: Azure Backup `(1)` takes a snapshot of your virtual machine and `(2)` sends, then stores the data as recovery points in geo-redundant recovery vaults. You dont have to wait for `(2)` to complete before attempting to restore. When you restore from a recovery point, you can restore your entire virtual machine or specific files only.

- **Azure Site Recovery**: Azure Site Recovery quickly and easily recover specific applications. It protects your virtual machines from a major disaster scenario when a whole region experiences an outage due to a major natural disaster or widespread service interruption. It replicates your virtual machines to a secondary region and orchestrates failover and failback to ensure business continuity. Azure Site Recovery provides disaster recovery as a service (DRaaS) for virtual machines, physical servers, Azure Stack VMs and even `AWS` VMs.

- **Azure managed disks - `snapshot`**: Azure managed disks provide a built-in backup feature that allows you to take snapshots of a particular managed disks. It takes snapshot of just one intended disk. You can use snapshots to create a point-in-time copy of your managed disk and restore it if needed. Snapshots are kept for `2days` by default, and can be extended to `5days`.

- **Azure managed disks - `image`**: This process captures a single image that contains all managed disks associated with a virtual machine, including both the operating system and data disks. You can use images to create new virtual machines with the same configuration as the original virtual machine.

**Steps to Backup a Virtual Machine**:
1. **Create a Recovery Services vault**: In the Azure portal, create a Recovery Services vault to store backup data. The vault must be created within your Azure subscription, and in the region where you want to store the data. Choose the storage redundancy option; `geo-redundant storage (GRS)` or `locally redundant storage (LRS)`. GRS is the default and best suited if Azure backup is your `primary` backup. 

2. **Define your backup policy optionsn**: In the Recovery Services vault, create a backup policy that defines the backup schedule, retention rules, and other settings. The policy specifies when to take the data snapshots, and how long to keep the snapshots. In your backup policy, you can specify to trigger a backup from one to five times per day. You can also enable encryption, compression, and other settings.

3. **Enable backup for the virtual machine**: The last step is to run the Azure Backup job process and create your backups. The `backup extension` requires the VM agent to be present, if the VM was migrated from on-premise and not naturally created on Azure , you need to install the agent.

4. **Restore data from a backup**: To restore data from a backup, you can use the Azure portal. After you back up your virtual machine, the backup snapshots and recovery points are stored in your Recovery Services vault. You can recover your machine by accessing the snapshot, or restore data to a specific point-in-time by using recovery points.

**Soft Delete**: Azure Backup provides protection against accidental or malicious deletion of your backup data by using soft delete. When you delete a backup item, the data is retained in the vault for 14 days. During this period, you can recover the deleted backup item without any additional cost. After 14 days, the data is permanently deleted and cannot be recovered.

- During the 14 day retention period, the Recovery Services vault shows your soft-deleted virtual machine with a red soft-delete icon.

- During the 14 day retention period, the Recovery Services vault shows your soft-deleted virtual machine with a red soft-delete icon.

- Before you can restore a soft-deleted virtual machine, you must undelete the backup data.

- When a Recovery Services vault contains any soft-deleted items, the vault can't be deleted. First delete or undelete all soft-deleted items, and then delete the vault.




- [Azure Virtual Machines Documentation](https://learn.microsoft.com/en-us/azure/virtual-machines/)
- [Virtual Machine Scale Set Documentation](https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/)
- [Azure Backup](https://learn.microsoft.com/en-us/azure/backup/)
- [App Service Documentation](https://learn.microsoft.com/en-us/azure/app-service/)
- [Containers On Windows Documentation](https://learn.microsoft.com/en-us/virtualization/windowscontainers/)
- [Interactive Lab: Create a Virtual Machine in Azure](https://learn.microsoft.com/en-us/training/modules/configure-virtual-machines/8-simulation-create-virtual-machines)
- [Interactive Lab: Create a Virtual Machine Scale Set in Azure](https://learn.microsoft.com/en-us/training/modules/configure-virtual-machine-availability/11-simulation-machine-scale)
- [Interactive Lab: Create an App Service in Azure](https://learn.microsoft.com/en-us/training/modules/configure-azure-app-services/11-simulation-web-apps)
- [Interactive Lab: Create a Container Group in Azure](https://learn.microsoft.com/en-us/training/modules/configure-azure-container-instances/6-simulation-containers)
- [Interactive Lab: Backup Virtual Machines](https://learn.microsoft.com/en-us/training/modules/configure-virtual-machine-backups/11-simulation-machine-backups)