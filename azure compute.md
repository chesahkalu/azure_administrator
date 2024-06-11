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

* | **Classification**     | **Description**                                                                                       | **Scenarios**                                                                                          |
|-------------------------|-------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **General Purpose**     | General-purpose virtual machines are designed to have a balanced CPU-to-memory ratio.                 | - Testing and development<br>- Small to medium databases<br>- Low to medium traffic web servers         |
| **Compute Optimized**   | Compute optimized virtual machines are designed to have a high CPU-to-memory ratio.                   | - Medium traffic web servers<br>- Network appliances<br>- Batch processes<br>- Application servers       |
| **Memory Optimized**    | Memory optimized virtual machines are designed to have a high memory-to-CPU ratio.                    | - Relational database servers<br>- Medium to large caches<br>- In-memory analytics                       |
| **Storage Optimized**   | Storage optimized virtual machines are designed to have high disk throughput and I/O.                 | - Big Data<br>- SQL and NoSQL databases<br>- Data warehousing<br>- Large transactional databases         |
| **GPU**                 | GPU virtual machines are specialized virtual machines targeted for heavy graphics rendering and video editing. Available with single or multiple GPUs. | - Model training<br>- Inferencing with deep learning                                                     |
| **High Performance Compute** | High performance compute offers the fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA). | - Workloads that require fast performance<br>- High traffic networks                                      |



- **Networking**: The virtual network and subnet where the virtual machine will be deployed. You can configure network security groups, public IP addresses, and other networking settings.

- **Storage**: The storage account and disk type for the virtual machine. You can choose between standard HDD, standard SSD, and premium SSD disks based on your performance requirements.

- **Operating system**: The operating system image that will be used to create the virtual machine. You can choose from a variety of `Windows` and `Linux images` available in the Azure Marketplace. Other images can include popular software tools such as SQL Server, SharePoint, and more. Optionally, you can bring your own custom image.

- **Pricing**: A subscription is billed two separate costs for every virtual machine: `compute and storage`. By separating these costs, you can scale them independently and only pay for what you need.
    * **Compute expenses**: are priced on a `per-hour` basis but billed on a `per-minute` basis. If the virtual machine is deployed for 55 minutes, you're charged for only 55 minutes of usage. With the `consumption-based` option, you pay for compute capacity by the second. You're able to increase or decrease compute capacity on demand and start or stop at any time. With the `reserved instances` option, you can save money by committing to a one- or three-year term for a discount on the compute resources.
    * **Storage expenses**: are billed separately from compute resources. You pay for the storage capacity you use, and the number of transactions performed on that storage. The storage costs are based on the type of storage you use, such as standard HDD, standard SSD, or premium SSD.
