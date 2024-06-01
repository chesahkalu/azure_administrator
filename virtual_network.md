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

* Azure creates default rules in a Security Group. Which allow `inbound` trafic only from your `Virtual Network and Load Balancer`, and `outbound` traffic to the `Internet and Virtual Network`. You can add more security rules to a network security group and select from a large variety of communication services, including HTTPS, RDP, FTP, and DNS, by specifying conditions for any of the following settings:
    - **Service** : The service specifies the destination protocol and port range for this rule. You can choose a predefined service, like RDP or SSH, or provide a custom port range
    - **Priority** : The priority of the rule. The lower the number, the higher the priority. The priority must be unique for each rule in the collection.
    - **Source (Any, IP addresses, Service tag)** : Controls `Inbound` traffic. Can be an IP address, a range of IP addresses, an application security group or a service tag. A service tag represents a group of IP address prefixes from a given Azure service.
    - **Destination (Any, IP addresses, Virtual network)** : Controls `Outbound` traffic. Properties similar to Source.
    - **Port** : The port number or range of port numbers for this rule. You can specify a single port number, a range of port numbers, or a combination of both.
    - **Protocol (Any, TCP, UDP)** : The protocol that this rule applies to. You can specify TCP, UDP, or Any.
    - **Action (Allow or Deny)** : The action to take when the rule matches. The action can be Allow or Deny. The default action is to deny traffic, and it takes precedence over the allow action.
    - **Description** : A description for this rule. Restricted to 140 characters.
    - **Name** : The name of the rule. Restricted to 80 characters.

* Each security rule is assigned a Priority value. All security rules for a network security group are processed in priority order. The lower the number, the higher the priority. The first rule that matches the traffic is applied, regardless of whether it allows or denies the traffic. If no rule matches, the default rule is applied. It's a good practice to leave gaps in your priority numbering, such as 100, 200, 300, and so. The gaps in the numbering allow you to add new rules without having to edit existing rules.

* You can't remove the default security rules. You can override a default security rule by creating another security rule that has a higher Priority setting for your network security group. By default, Azure allows virtual machines in the same subnet to send traffic to each other (referred to as intra-subnet traffic). You can prohibit intra-subnet traffic by defining a rule in the network security group to deny all inbound and outbound traffic. This rule prevents all virtual machines in your subnet from communicating with each other.

* For inbound traffic, Azure first checks the NSG rules associated with the subnet to ensure that the traffic is allowed to enter the subnet, After the traffic passes the subnet rules, Azure then checks the NSG rules associated with the network interface(NIC)`(point of connection, like an Network card with with an associated IP adress)` of the target VM or resource. This second check ensures that the traffic is specifically allowed to reach the intended resource. The reverse process occurs for outbound traffic. This process ensures layered security for your resources.

### Scenario: 
- Create and configure network security groups.
- Associate network security groups to virtual machines.
- Deny and allow access to the virtual machines by using network security groups.

### Solution:
1. Create a virtual machine.
    - Create a Windows Server virtual machine.
    - Select `Inbound port rules` as none, this excludes the basic rule of Remote Desktop Protocol (RDP)connection port 3389 aswell as any other connection.
    - On the `Networking` tab, select `none` for the network security group. This action ensures that the virtual machine has no network security group associated with it.
    - On disable `Boot diagnostics` to allow the virtual machine to boot up without requiring some additional configurations.
    - Verify the virtual machine is created.
    - Review the Inbound port rules tab, and note there are no network security groups associated with the virtual machine.


2. Create a network security group and associate the group with the virtual machine.
    - Create a network security group.
    - Go to `Network Interfaces` and associate the network security group with the virtual machine network interface (NIC). This action applies the network security group rules to the virtual machine through the NIC, not subnet.

3. Create a security rule to allow RDP access to the virtual machine.
    - Try to connect to the virtual machine using RDP. The connection should fail because the network security group denies the RDP connection.
    - Add an inbound port rule to allow RDP to the virtual machine on port 3389, TCP protocol, priority 300 and name it `Allow-RDP`.
    - Verify that the security rule is applied to the network security group associated with the virtual machine and you can now connect to the virtual machine using RDP.
    - To use RDP download the RDP file from the Azure portal and open it with the Remote Desktop Connection application.

4. Configure an outbound security port rule to deny internet access.
    - You already have an outbound security rule that allows all traffic to the internet. Remember this is a default rule that cant be reomved. Verify that you can access the internet from the virtual machine.
    - Add an outbound security rule to deny all traffic to the internet. This rule should then have a higher priority than the default rule to be able to override it.
    - Verify that you can no longer access the internet from the virtual machine.


## Application Security Groups (ASG)
Application Security Groups (ASGs) let you organize virtual machines into groups based on workload or function, eg. Webservers, Databases. Instead of managing security rules for each VM individually, you can apply security rules to the entire group having same functions. This means you can define a security policy once for an `application group`, and it applies to all VMs within that group. With this You can define fine-grained network security policies based on workloads, rather than explicit IP addresses. ASGs enable you to configure network security as a natural extension of an application's structure, allowing you to group virtual machines with similar security requirements. 
**Scenario**
- We have six virtual machines in our configuration with two web servers and two database servers.
- Customers access the online catalog hosted on our web servers.
- The web servers must be accessible from the internet over HTTP port 80 and HTTPS port 443.
- Inventory information is stored on our database servers.
- The database servers must be accessible over HTTPS port 1433.
- Only our web servers should have access to our database servers.
**Solution**:
1. Create Application Security Groups for the Virtual Machines
    - Create an application security group named **WebASG** to group our web server machines.
    - Create an application security group named **DBASG** to group our database server machines.

2. Assign the Network Interfaces for the Virtual Machines
    - For each virtual machine server, assign its NIC to the appropriate application security group.

3. Create the Network Security Group and Security Rules
    * Rule 1
        - **Priority**: 100
        - **Description**: Allow access from the internet to machines in the WebASG group from HTTP port 80 and HTTPS port 443.
        - **Note**: Rule 1 has the lowest priority value, so it has precedence over the other rules in the group. Customer access to our online catalog is paramount in our design.

    * Rule 2
        - **Priority**: 110
        - **Description**: Allow access from machines in the WebASG group to machines in the DBASG group over HTTPS port 1433.

    * Rule 3
        - **Priority**: 120
        - **Description**: Deny access from anywhere to machines in the DBASG group over HTTPS port 1433.

**Note**: The combination of Rule 2 and Rule 3 ensures that only our web servers can access our database servers. This security configuration protects our inventory databases from outside attack.


