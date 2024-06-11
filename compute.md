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

- **Monitoring**: You can monitor the performance and health of your virtual machine using Azure Monitor. You can set up alerts, view metrics, and analyze performance data.

- **Security**: You can configure security settings, network security groups, and encryption for your virtual machine. You can also enable Azure Security Center for advanced threat protection.

- **Automation**: You can automate management tasks using Azure Automation, Azure Functions, or other automation tools. You can create runbooks, scripts, and workflows to streamline operations.

- **Scaling**: You can scale virtual machines manually or automatically based on demand. You can use Azure Autoscale to automatically adjust the number of VM instances based on predefined rules.

- **High Availability**: You can configure availability sets, availability zones, or virtual machine scale sets for high availability and fault tolerance. You can distribute VM instances across multiple fault domains and update domains to ensure uptime. 


## 




- [Interactive Lab: Create a Virtual Machine in Azure](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%209)