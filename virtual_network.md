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

### Steps to Create a Virtual Network

1. Navigate to the Azure portal and search for `Virtual networks`.
2. Click on `+ Create` to create a new virtual network.
3. Fill in the required basic details like `Name`, `Region`.
4. Configure security settings according to your requirements.
5. Configure your virtual network address space with the IPv4 and IPv6 addresses and subnets you need.
   - Define the address space of your virtual network with one or more IPv4 or IPv6 address ranges. 
   - Create subnets to segment the virtual network address space into smaller ranges for use by your applications. 
   - When you deploy resources into a subnet, Azure assigns the resource an IP address from the subnet.
6. Review and create the virtual network.

## Network Security Groups (NSG)

Network security groups (NSGs) are a simple way to filter network traffic to and from Azure resources in an Azure virtual network. Each network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, several types of Azure resources. You can assign network security groups to a subnet and create a protected screened subnet (also referred to as a demilitarized zone or DMZ). A DMZ acts as a buffer between resources within your virtual network and the internet.

### Steps to Create a Network Security Group

* Azure creates default rules in a Security Group. Which allow `inbound` trafic only from your `Virtual Network and Load Balancer`, and `outbound` traffic to the `Internet and Virtual Network`. You can add more security rules to a network security group by specifying conditions for any of the following settings:

    - Name
    - Priority
    - Port
    - Protocol (Any, TCP, UDP)
    - Source (Any, IP addresses, Service tag)
    - Destination (Any, IP addresses, Virtual network)
    - Action (Allow or Deny)

* Each security rule is assigned a Priority value. All security rules for a network security group are processed in priority order. The lower the number, the higher the priority. The first rule that matches the traffic is applied, regardless of whether it allows or denies the traffic. If no rule matches, the default rule is applied. It's a good practice to leave gaps in your priority numbering, such as 100, 200, 300, and so. The gaps in the numbering allow you to add new rules without having to edit existing rules.

* You can't remove the default security rules. You can override a default security rule by creating another security rule that has a higher Priority setting for your network security group. By default, Azure allows virtual machines in the same subnet to send traffic to each other (referred to as intra-subnet traffic). You can prohibit intra-subnet traffic by defining a rule in the network security group to deny all inbound and outbound traffic. This rule prevents all virtual machines in your subnet from communicating with each other.

* For inbound traffic, Azure first checks the NSG rules associated with the subnet to ensure that the traffic is allowed to enter the subnet, After the traffic passes the subnet rules, Azure then checks the NSG rules associated with the network interface`(point of connection, like an Network card with with an associated IP adress)` of the target VM or resource. This second check ensures that the traffic is specifically allowed to reach the intended resource. The reverse process occurs for outbound traffic. This process ensures layered security for your resources.



