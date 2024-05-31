# Configure and manage virtual networks

## Pre-requisites

- Understanding of Azure fundamentals
- An Azure account with an active subscription (Free tier is enough). Sign up or login to your Azure account [here](https://azure.microsoft.com/en-us/free/)
- Basic knowledge of networking concepts

## Overview

A virtual network is like a digital version of a physical network. Azure Virtual Network allow different Azure resources to securely communicate with each other, the internet, and on-premises networks. When you create a virtual network, your services and virtual machines within your virtual network can communicate directly and securely with each other in the cloud. You can still configure endpoint connections for the virtual machines and services that require internet communication, as part of your solution.

- Subnets: After creating a virtual network, you can add one or more subnets in each virtual network. Subnets enable you to segment the virtual network IP address into one or more sub-networks and allocate a portion of the virtual network's address space to each subnet. You can then deploy Azure resources in a specific subnet. Azure reserves five IP addresses, The first four addresses and the last address are reserved.

- Static IP addresses: Static addresses are assigned when a public IP address is created. Static addresses aren't released until a public IP address resource is deleted. If the address isn't associated to a resource, you can change the assignment method after the address is created. If the address is associated to a resource, you might not be able to change the assignment method. You select and assign any unassigned or unreserved IP address in the subnet's address range.
Suppose a subnet's address range is 10.0.0.0/16, and addresses 10.0.0.4 through 10.0.0.9 are already assigned to other resources. In this scenario, you can assign any address between 10.0.0.10 and 10.0.255.254.

- Dynamic IP addresses: Dynamic addresses are assigned after a public IP address is associated to an Azure resource and is started for the first time. Dynamic addresses can change if a resource such as a virtual machine is stopped (deallocated) and then restarted through Azure. The address remains the same if a virtual machine is rebooted or stopped from within the guest OS. When a public IP address resource is removed from a resource, the dynamic address is released. Azure assigns the next available unassigned or unreserved IP address in the subnet's address range. Dynamic assignment is the default allocation method. Suppose addresses 10.0.0.4 through 10.0.0.9 are already assigned to other resources. In this case, Azure assigns the address 10.0.0.10 to a new resource.

## Steps to Create a Virtual Network

1. Navigate to the Azure portal and search for `Virtual networks`.
2. Click on `+ Create` to create a new virtual network.
3. Fill in the required basic details like `Name`, `Region`.
4. Configure security settings according to your requirements.
5. Configure your virtual network address space with the IPv4 and IPv6 addresses and subnets you need.
   - Define the address space of your virtual network with one or more IPv4 or IPv6 address ranges. 
   - Create subnets to segment the virtual network address space into smaller ranges for use by your applications. 
   - When you deploy resources into a subnet, Azure assigns the resource an IP address from the subnet.
6. Review and create the virtual network.



