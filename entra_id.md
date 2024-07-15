# Manage Microsoft Entra ID

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Introduction](#introduction) 
- [Create a tenant](#create-a-tenant)
- [Add Users](#add-users)
- [Add Groups](#add-groups)
- [Guest Users](#guest-users)
- [Devices](#devices)
- [Licenses](#licenses)
- [Conclusion](#conclusion)
- [References and Further Reading](#references-and-further-reading)

---

## Prerequisites

- An active Azure subscription. [Sign up for a free tier here](https://azure.microsoft.com/en-us/free/).

---

## Introduction


[Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/fundamentals/whatis) an identity and access management service that helps you manage employee access to corporate resources. It simplifies the process of managing users, while establishing access and roles to this users. This guide will walk you through the process of creating, configuring, and managing Microsoft Entra ID.

Entra ID is a standalone service that can be used with other Microsoft services like Azure, Microsoft 365, and Dynamics 365. It provides a single sign-on experience for users, allowing them to access multiple applications and services with a single set of credentials. Entra ID also provides security features like multi-factor authentication, conditional access, and identity protection to help protect your organization's data.

Some key Terminologies to note are:
- Member Users: A member user account is a native member of the Microsoft Entra organization that has a set of default permissions like being able to manage their profile information. When someone new joins your organization, they typically have this type of account created for them.
- Guest Users: A guest user account is an external user who has been invited to the organization. They can be invited to collaborate on projects, share files, or access resources. Guest users are not members of the organization and do not have the same permissions as member users.
- Tenant: A tenant is a representation of an organization. `It's a dedicated and trusted instance of the Microsoft Entra service` that an organization receives and owns when it signs up for a Microsoft Entra subscription. Each tenant has its own users, groups, resources, and settings.
- Group: A group is a collection of users who have the same access permissions and roles to resources. Groups can be used to manage access to resources, share information, and collaborate on projects.
- Role: A role is a collection of permissions that can be assigned to users or groups. Roles define what users can do within the organization, such as managing users, accessing resources (Role-based access control), or configuring settings.
- Administrator Role: An administrator role is a special role that grants users full access to the Microsoft Entra organization. Administrators can manage users, groups, resources, and settings, as well as configure security and compliance settings.

---

### Create a tenant

Normally, when you sign up for an Azure subscription, a tenant is created for you. However, you can create additional tenants if needed. Here's how you can create a new tenant:
1. Sign in to your Azure portal. You need an active subscription to be able to create a new tenant.
2. On the Azure Portal Home page, from the left hand menu bar, click and select `Microsoft Entra ID`
3. On the top menu of the page, click `Manage Tenants` to view your available tenants and then click `create` to add a new tenant.
4. On the `create a tenant`, select `Microsoft Entra ID` as tenant type, click configuration to configure an organization name and unique domain name.
5. Review and create.
6. On the  left menu pane, click `licenses` , on this page click `All products` on the left pane, then click `Try/Buy` to activate a free trial for Microsoft Entra ID P1 or P2. This will enable you to use dynamic assignment to add members to groups automatically based on a rule that you define, as well as other features.

---

### Add Users

You can add users to your Microsoft Entra ID organization in the following ways:
1. **Add a member user**: A user is a native member of the organization. To add a member user, follow these steps:
    - On the Microsoft Entra ID page, click `Users` on the left menu pane under manage, the `All Users` pane comes up
    - In the top menu bar, select `New user`, then select `Create new user` in the drop-down.
    - In the `Create New user` pane, Fill in the user's details, such as user principal name (user1@tenantname.onmicrosoft.com), first name, last name, and password.
    - Select Review + Create, then select Create. The All users pane reappears for the current Tenant - Microsoft Entra ID. The user is now created and registered to your organization.
    - The user can now sign in to the Microsoft Entra ID portal using the user principal name and password you provided.

2. **Delete a user**: To delete a user, follow these steps:
    - On the Microsoft Entra ID page, click `Users` on the left menu pane under manage, the `All Users` pane comes up
    - In the `All Users` pane, select the user you want to delete.
    - In the top menu bar, select `Delete user`, then select `Delete Again` in the confirmation pane.

3. **Restore a deleted user**: To restore a deleted user, follow these steps:
    - On the Microsoft Entra ID page, click `Users` on the left menu pane under manage, the `All Users` pane comes up
    - In the `All Users` pane, click `Deleted users` to view the list of deleted users that were deleted within the last `30` days.
    - In the `Deleted users` pane, select the user you want to restore.
    - In the top menu bar, select `Restore user`, then select `Restore` in the confirmation pane.

---

### Add Groups

- You want to be able to give a group of users (like developers) the same access permissions and roles to resources.
- There two types of groups in Microsoft Entra ID: `Security groups`(used for assigning permissions to resources) and `Microsoft 365 groups`(used for collaboration and sharing resources).
- Adding members to a group to give access are of two types: 
    - **Dynamic User**: Members are added to a group automatically based on a rule that you define. If a user meets the criteria of the rule, they are added to the group. If they no longer meet the criteria, they are removed from the group.
    - **Assigned User**: Members are added manually.

To add a group, follow these steps:
1. On the Microsoft Entra ID page, click `Groups` on the left menu pane under manage, the `All Groups` pane comes up
2. In the top menu bar, select `New group`, the `New group` page comes up. Select `Security` , Name the group `Developers`, add a description `Development team`.
3. Select `Create`. The `Groups` | `All groups` pane appears, including the new group in the list of Groups. You might need to refresh to see your new group.

- Use direct assignment to add members to the group manually.
4. To add members to the group, select the group you created, click `Members` on the left menu pane, then click `Add members` in the top menu bar.
5. In the `Add members` pane, search for the user you want to add to the group, select the user, then click `Select`. You'll see this user in the `Direct members` list for the Developers group in the Members pane. You might need to refresh to see the users. You can add multiple users to the group this way. You can also add a group as a member of another group, this is called nested groups and adds all the members of the nested group to the parent group.

- Use dynamic assignment to add members to the group automatically based on a rule that you define. Membership then depends on whether a user meets the rules you set for the group. If you didn't activate the free trial for Microsoft Entra ID P1 or P2, you won't be able to use dynamic assignment.

6. In the left menu pane, under Manage, select `Properties`. The Properties pane appears for your developer group.
7. Change Membership type to `Dynamic User`.
8. Under Dynamic user members, select the `Add dynamic query` link. The Dynamic membership rules pane appears.
9. On the Configure Rules tab, select the following values for the rule:
    - Property: JobTitle
    - Operator: Equals
    - Value: Developer
The membership of this group now depends on whether the user is a developer. You can also use other properties to define rules for dynamic membership, such as department, location or user type.
10. Select `Save`. The Dynamic membership rules pane closes, and the `Properties` pane for your group appears.

---

### Guest Users

Guest users are external users who have been invited to the organization from anoth Azure AD tenant or from a Microsoft account. They can be invited to collaborate on projects, share files, or access resources and applications. With `Microsoft Entra business to business (B2B)`, you can add people from other companies to your Microsoft Entra tenant as `guest users`. You can grant `guest users` access with the appropriate restrictions in place, then remove access when the work is done. Use the Azure portal to invite business-to-business (B2B) collaboration users. You can invite guest users to a Microsoft Entra organization, group, or application. After you invite a user, their account is added to Microsoft Entra ID, with a guest user type. After you add a guest user to the organization, send them a direct link to a shared app. Have the guest user open the redemption URL in the invitation email.

- To invite a guest user, follow these steps:
1. On the Microsoft Entra ID page, click `Users` on the left menu pane under manage, the `All Users` pane comes up. In the top menu bar, select `New user`, then select `Invite External user` in the drop-down. 
2. In the `Invite External user` pane, fill in the user's details, such as email address, display name, last name, and invite message.
3. Select `Review + invite`, then select `Invite`. An invitation is sent to the email address you provided for the guest user. The All users pane appears. Notice that the user now appears in the list of users and has Guest as User type. You might need to refresh to see the new user. 
4. The guest user can now sign in to the Microsoft Entra ID portal using the email address provided. The guest user can access the `resources` you shared with them and can be added to `groups` and `enterprise applications` to collaborate on projects

---

---

### Devices

- Devices are objects in Microsoft Entra ID that represent physical devices, such as computers, tablets, and smartphones. Devices can be registered with Microsoft Entra ID to enable features like conditional access, device-based authentication, and device management. You can manage devices in Microsoft Entra ID by performing tasks like registering devices, viewing device details, and removing devices from the organization.

- There are three ways to get a device identity:

    1. `Microsoft Entra registration`: This is the most secure way to register a device with Microsoft Entra ID. When a device is registered with Microsoft Entra ID, it gets a unique identity that can be used to enforce conditional access policies and manage device settings. `In these scenarios, a user can access your organization's resources using a personal device`. To register a device with Microsoft Entra ID, you need to sign in to the device using your Microsoft Entra ID credentials.
    2.  `Microsoft Entra join`: This is a way to join a device to an on-premises Active Directory domain and register it with Microsoft Entra ID at the same time. When a device is Microsoft Entra joined, it gets a unique identity in Microsoft Entra ID that can be used to enforce conditional access policies and manage device settings. Microsoft Entra join is typically used for devices that are managed by an organization and need to access Microsoft Entra ID resources.
    3. `Microsoft Entra hybrid join`

---

### Licenses

- Licenses in Microsoft Entra ID are used to assign specific features and services to users. Licenses can be assigned to individual users or groups of users to enable or disable specific features and services. Licenses can be assigned manually or automatically based on user properties or group membership. You can view and manage licenses in Microsoft Entra ID by performing tasks like assigning licenses, removing licenses, and viewing license details.

- Types of licenses in Microsoft Entra ID include:
    - `Microsoft Entra ID Free`: This license provides basic features like user management, group management, and single sign-on. It is free and available to all Microsoft Entra ID users.
    - `Microsoft Entra ID Premium P1`: This license provides advanced features like self-service password reset, multi-factor authentication, and conditional access. It is available as a standalone license or as part of the Microsoft 365 Business Premium plan.
    - `Microsoft Entra ID Premium P2`: This license provides additional features like identity protection, privileged identity management, and access reviews. It is available as a standalone license or as part of the Microsoft 365 E5 plan.

---

### SSPR

- Self-service password reset (SSPR) is a feature that enables users to reset their passwords without the need for administrator intervention. This feature can help reduce the number of help desk calls related to password resets and improve user productivity. 

- In Microsoft Entra ID, any user can change their password if they're already signed in. But if they're not signed in and forgot their password or it's expired, they'll need to reset their password. With SSPR, users can reset their passwords in a web browser or from a Windows sign-in screen to regain access to Azure, Microsoft 365, and any other application that uses Microsoft Entra ID for authentication.

- Some requirements for SSPR include:
    - a non-administrative user accountUsers with a valid email address in their profile.
    - a Microsoft Entra organization: This organization must have at least a trial license enabled.
    - a Microsoft Entra account with Global Administrator privileges: You'll use this account to set up SSPR.
    - Entra ID Premium P1 or P2 license is required.
    - SSPR must be enabled for your organization.
- To enable SSPR for your organization, follow these steps:
    1. Go to the Azure portal, go to Microsoft Entra ID > Password reset.

    2. Properties:
        - Enable SSPR.
        - You can enable it for all users in the Microsoft Entra organization or for selected users.
        - To enable for selected users, you must specify the security group. Members of this group can use SSPR.
    3. Authentication methods:
        - Choose whether to require one or two authentication methods.
        - Choose the authentication methods that the users can use.
    4. Registration:
        - Specify whether users are required to register for SSPR when they next sign in.
        - Specify how often users are asked to reconfirm their authentication information.
    5. Notifications: Choose whether to notify users and administrators of password resets.
    6. Customization: Provide an email address or web page URL where your users can get help.

---

## Conclusion

Microsoft Entra ID simplifies the process of managing users, while establishing access and roles to these users. By following the steps outlined in this guide, you can create, configure, and manage users, groups, tenants, and guest users in Microsoft Entra ID. This will help you streamline your Azure infrastructure management and ensure consistency across your organization.

## References and Further Reading

- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/entra/fundamentals/whatis)
- [Microsoft Entra ID for Developers](https://learn.microsoft.com/en-us/entra/identity-platform/)
- [How to: Assign or remove Microsoft Entra ID licenses](https://learn.microsoft.com/en-us/entra/fundamentals/license-users-groups)
- [SSPR](https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-enable-sspr)

