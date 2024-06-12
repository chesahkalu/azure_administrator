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









- [Interactive Lab: Create a Virtual Machine in Azure](https://mslearn.cloudguides.com/en-us/guides/AZ-900%20Exam%20Guide%20-%20Azure%20Fundamentals%20Exercise%209)
- [Interactive Lab: Create a Virtual Machine Scale Set in Azure](https://learn.microsoft.com/en-us/training/modules/configure-virtual-machine-availability/11-simulation-machine-scale)
