# Guide to Hands-On Azure Administration Through Project-Based Learning 

This repository is designed for those seeking practical, project-based experience in Azure Administration. It includes a variety of projects that reflect the daily tasks of an Azure administrator, making it an invaluable resource for gaining hands-on experience and preparing for the Azure Administrator certification exam. Additionally, it serves as my personal project portfolio and documentation.

---

![Azure Administration](resources/azure-administrator-associate-600x600.png)

---

## Table of Contents
1. [Requirements](#requirements)
2. [Project Links](#project-links)
3. [Azure Skills Required for an Azure Administrator:](#azure-skills-required-for-an-azure-administrator)
    - [Manage Azure identities and governance](#manage-azure-identities-and-governance)
    - [Implement and manage storage](#implement-and-manage-storage)
    - [Deploy and manage Azure compute resources](#deploy-and-manage-azure-compute-resources)
    - [Implement and manage virtual networking](#implement-and-manage-virtual-networking)
    - [Monitor and maintain Azure resources](#monitor-and-maintain-azure-resources)

---

![Azure Administration](https://img.shields.io/badge/Azure-Administration-blue)

## Requirements
- Understanding of Azure fundamentals
- An Azure account with an active subscription (Free tier is enough). Sign up or log in to your Azure account [here](https://azure.microsoft.com/en-us/free/)

---

![Azure Administration](https://img.shields.io/badge/Azure-Administration-blue)

## Project Links

| **Title** | **Description** | **Link** |
| --------- | --------------- | -------- |
| **Azure Resource Management** | Generate an ARM template from an existing resource on the portal to deploy a new similar resource | [Project](./arm_template.md) |
| **Manage Microsoft Entra ID**  | Create, configure, and manage Azure Active Directory Access, Users, Groups, Tenants, and Guest users in Microsoft Entra ID | [Project](./entra_id.md) |
| **Azure Compliance and Governance** | Learn to navigate and apply Azure's governance tools, focusing on policy creation and compliance management using resource tagging | [Project](./policy_compliance_with_tags.md) |
| **RBAC-Subscription-Management Groups** | Implement Role-Based Access Control (RBAC) in Azure to manage user permissions and access to resources, Manage subscriptions using Management Groups | [Project](./rbac.md) |
| **Azure Virtual Network** | Create and configure Virtual Network in Azure, including Subnets, Network Security Groups, Routing, Peering, VPN Gateways, Application Gateway, and Load Balancer | [Project](./virtual_network.md) |
| **Azure Compute** | Create and manage Virtual Machines, Virtual Machine Scale Sets, Azure App Service, Azure Container Instances, and Azure Backups | [Project](./compute.md) |
| **Azure Monitoring and Diagnostics** | Monitor and diagnose Azure resources using Azure Monitor, Log Analytics, Application Insights, and Azure Service Health | [Project](./monitoring_diagnostics.md) |

---

![Azure Administration](https://img.shields.io/badge/Azure-Administration-blue)

## Azure Skills Required for an Azure Administrator:

### Manage Azure identities and governance

#### Manage Azure AD users and groups
- Create users and groups
- Manage user and group properties
- Manage licenses in Azure AD
- Manage external users
- Configure self-service password reset (SSPR)

#### Manage access to Azure resources
- Manage built-in Azure roles
- Assign roles at different scopes
- Interpret access assignments

#### Manage Azure subscriptions and governance
- Implement and manage Azure Policy
- Configure resource locks
- Apply and manage tags on resources
- Manage resource groups
- Manage subscriptions
- Manage costs by using alerts, budgets, and Azure Advisor recommendations
- Configure management groups

---

### Implement and manage storage

#### Configure access to storage
- Configure Azure Storage firewalls and virtual networks
- Create and use shared access signature (SAS) tokens
- Configure stored access policies
- Manage access keys
- Configure identity-based access for Azure Files

#### Configure and manage storage accounts
- Create and configure storage accounts
- Configure Azure Storage redundancy
- Configure object replication
- Configure storage account encryption
- Manage data by using Azure Storage Explorer and AzCopy

#### Configure Azure Files and Azure Blob Storage
- Create and configure a file share in Azure Storage
- Create and configure a container in Blob Storage
- Configure storage tiers
- Configure snapshots and soft delete for Azure Files
- Configure blob lifecycle management
- Configure blob versioning

---

### Deploy and manage Azure compute resources

#### Automate deployment of resources by using Azure Resource Manager (ARM) templates or Bicep files
- Interpret an ARM template or a Bicep file
- Modify an existing ARM template
- Modify an existing Bicep file
- Deploy resources by using an ARM template or a Bicep file
- Export a deployment as an ARM template or compile a deployment as a Bicep file

#### Create and configure virtual machines
- Create a virtual machine
- Configure Azure Disk Encryption
- Move a virtual machine to another resource group, subscription, or region
- Manage virtual machine sizes
- Manage virtual machine disks
- Deploy virtual machines to availability zones and availability sets
- Deploy and configure an Azure Virtual Machine Scale Sets

#### Provision and manage containers in the Azure portal
- Create and manage an Azure container registry
- Provision a container by using Azure Container Instances
- Provision a container by using Azure Container Apps
- Manage sizing and scaling for containers, including Azure Container Instances and Azure Container Apps

#### Create and configure Azure App Service
- Provision an App Service plan
- Configure scaling for an App Service plan
- Create an App Service
- Configure certificates and TLS for an App Service
- Map an existing custom DNS name to an App Service
- Configure backup for an App Service
- Configure networking settings for an App Service
- Configure deployment slots for an App Service

---

### Implement and manage virtual networking

#### Configure and manage virtual networks in Azure
- Create and configure virtual networks and subnets
- Create and configure virtual network peering
- Configure public IP addresses
- Configure user-defined network routes
- Troubleshoot network connectivity

#### Configure secure access to virtual networks
- Create and configure network security groups (NSGs) and application security groups
- Evaluate effective security rules in NSGs
- Implement Azure Bastion
- Configure service endpoints for Azure platform as a service (PaaS)
- Configure private endpoints for Azure PaaS

#### Configure name resolution and load balancing
- Configure Azure DNS
- Configure an internal or public load balancer
- Troubleshoot load balancing

---

### Monitor and maintain Azure resources

#### Monitor resources in Azure
- Interpret metrics in Azure Monitor
- Configure log settings in Azure Monitor
- Query and analyze logs in Azure Monitor
- Set up alert rules, action groups, and alert processing rules in Azure Monitor
- Configure and interpret monitoring of virtual machines, storage accounts, and networks by using Azure Monitor Insights
- Use Azure Network Watcher and Connection Monitor

#### Implement backup and recovery
- Create a Recovery Services vault
- Create an Azure Backup vault
- Create and configure a backup policy
- Perform backup and restore operations by using Azure Backup
- Configure Azure Site Recovery for Azure resources
- Perform a failover to a secondary region by using Site Recovery
- Configure and interpret reports and alerts for backups

