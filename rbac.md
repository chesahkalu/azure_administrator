# Managing Azure Role-Based Access Control and Subscriptions with Management Groups

---

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Create a Management Group](#create-a-management-group)
4. [Role-Based Access Control (RBAC)](#role-based-access-control-rbac)
5. [Assigning Roles to Users](#assigning-roles-to-users)
6. [Conclusion](#conclusion)
7. [References and Further Reading](#references-and-further-reading)

---

## Introduction

- `Role-Based Access Control (RBAC)` is a fundamental aspect of Azure administration, allowing you to manage user permissions and access on resources.
- `Subscriptions` are the fundamental unit of billing in Azure, grouping resources and services for billing and access control.
- `Management groups` provide a hierarchy for managing access, policies, and compliance across your Azure subscriptions, essential for large-scale governance. It starts with the `root management group`, which represents the top-level of the hierarchy.

---

## Prerequisites

- An understanding of Azure fundamentals; Understanding how resources are organized, deployed, and managed.
- Microsoft Entra ID concepts; Understanding of Azure Active Directory, users, groups, and roles.
- An active Azure subscription. [Sign up for a free tier here](https://azure.microsoft.com/en-us/free/).

---

## Create a Management Group
The core concept of `Management Groups` is to provide a level of organization above subscriptions. This allows you to manage access, policies, and compliance across multiple subscriptions. The `root management group` is the top-level of the hierarchy, and all other `management groups` and `subscriptions` are nested within it.

The core 3 things you can assign to a `Management Group` that will apply to all subscriptions and management groups within it are:

- **Access Control**: Apply access controls to multiple subscriptions and management groups. This allows you to manage who can access and manage resources at different levels of the hierarchy.

- **Policy Assignment**: Assign policies to multiple subscriptions and management groups. Policies are used to enforce rules and effects on resources, so they stay compliant with corporate standards.

- **Budgets**: Apply budgets to multiple subscriptions and management groups. Budgets allow you to track costs and alert you when costs exceed a certain threshold.

**To create a management group:**

1. Navigate to the Azure portal and search for `Management groups`.
2. Click on `+ Create` to create a new management group. If the option is disabled, you may need appropriate permissions. To set up a management group, you need to be a `User Access Administrator` or `Owner` at the root management group level. For a simple azure account created for learning purposes, you may have the necessary permissions, if not:

    - Go to `Microsoft Entra ID`.
    - Select `Properties` on the left pane.
    - Scroll down and select `Yes` for "can manage access to all Azure subscriptions and management groups in this tenant".

3. Click on the created management group to view its details, and click on `+ Add subscription` to add a subscription to the management group.
4. Clikc on the Subcription to view its details and copy the `Subscription ID` for implementing `RBAC`.

---

## Role-Based Access Control (RBAC)

- The following table describes the core concepts of Azure RBAC:

| **Concept** | **Description** | **Example** |
| ----------- | --------------- | ----------- |
| Security Principal | Represents a user, group, or service principal that is assigned a role. | User, group, service principal, managed identity |
| Role | Defines a set of permissions that can be assigned to a security principal. | Some built-in role definitions: Owner, Contributor, Reader, Custom role |
| Scope | Defines the set of resources that the role applies to. Setting the boundary for the requested level of access, or "how much" access is granted. | Subscription, resource group, resource |
| Role Assignment | Links a security principal to a role, within a specific scope. | UserA is assigned the Contributor role for ResourceGroup1 |

- Azure includes several built-in roles that you can use. The following lists four fundamental built-in roles:

| **Role Name** | **Description** | **Actions** |
| ---------| --------------- | ----------- |
| Owner | Full access to all resources, including the right to delegate access to others. | `Microsoft.Authorization/*` |
| Contributor | Can create and manage all types of Azure resources, but can’t grant access to others. | `Microsoft.Authorization/*/Write` |
| Reader | View resources, but cannot make changes. | `Microsoft.Authorization/*/Read` |
| User Access Administrator | Manage user access to resources. | `Microsoft.Authorization/*/Write` |

- If the built-in roles don't meet the specific needs of your organization, you can create your own custom roles.

**A role definition consists of sets of permissions that are defined in a JSON file. Each permission set has a name, such as Actions or NotActions that describe the permissions. Some examples of permission sets include:**

- Actions permissions identify what actions are allowed. (For example, read or write.)

- NotActions permissions specify what actions aren't allowed. (For example, delete or write.)

- DataActions permissions indicate how data can be changed or used. (For example, read, write, or delete.)

- AssignableScopes permissions list the scopes where a role definition can be assigned. (For example, a role definition can be assigned to a subscription, resource group, or resource.)

![alt text](/resources/image.png)

The Actions permissions show the Contributor role has all action privileges. The asterisk "*" wildcard means "all." The NotActions permissions narrow the privileges provided by the Actions set, and deny three actions:

- Authorization/*/Delete: Not authorized to delete or remove for "all."
- Authorization/*/Write: Not authorized to write or change for "all."
- Authorization/elevateAccess/Action: Not authorized to increase the level or scope of access privileges.

The Contributor role also has two permissions to specify how data can be affected:

- "NotDataActions": []: No specific actions are listed. Therefore, all actions can affect the data.
- "AssignableScopes": ["/"]: The role can be assigned for all scopes that affect data.

Use the Actions and NotActions permissions together to grant and deny the exact privileges for each role. The Actions permissions can provide the breadth of access and the NotActions permissions can narrow the access.

---

## Assigning Roles to Users

1. Create a JSON file with the role definition that allows a user to create support requests. The role should allow the user to can view resource groups in a specific subscription, but not the resources in the resource groups. The [role_definition.json](/resources/role_definition.json) should look like this :

```json
{
    "properties": {
        "roleName": "Support Request Contributor (Custom)",
        "description": "Allows to create support requests",
        "assignableScopes": [
            "/providers/Microsoft.Management/managementGroups/MANAGEMENT_GROUP_ID",
            "/subscriptions/SUBSCRIPTION_ID"
        ],
        "permissions": [
            {
                "actions": ["Microsoft.Resources/subscriptions/resourceGroups/read",
                "Microsoft.Support/*"],
                "notActions": [],
                "dataActions": [],
                "notDataActions": []
            }
        ]
    }
}
```
- The `Microsoft.Resources/subscriptions/resourceGroups/read` action allows the user to view resource groups in a specific subscription. The specific subscription is identified by the `SUBSCRIPTION_ID` placeholder in the `Assignablescopes` section. Replace `SUBSCRIPTION_ID` with the actual subscription ID and `MANAGEMENT_GROUP_ID` with the management group ID.
- The `Microsoft.Support/*` action allows the user to create support requests.

2. Upload the role definition to Azure.

- Search for `Management groups` in the Azure portal and click on the management group where you want to assign the role.
- Click on `Access control (IAM)` on the left pane and then `+ Add` and click `Add Custom role` to add the custom role assignment.
- You can build the role assignment by following the steps on the page and filling the fields, Or you can upload the JSON file by clicking on `Start from JSON` and selecting the `role_definition.json` file. This will automatically populate the fields with the role definition.
- Click `Next` as the fields populate and then `Review + Create`.

3. Assign the role to a user.

- On the `Access control (IAM)` page, click on `+ Add`  and click on ` Add a role assingment`.
- Search for the name of the role you uploaded `Support Request Contributor (Custom)`, and select it.
- Click `Next` and Click on `Select members` to search for the user you want to assign the role to. You can review how to create a user in Microsoft Entra ID [here](./entra_id.md).
- Search and select the user and click `Next` and then `Review + Assign` to assign the role to the user.

4. Verify the role assignment.

- Log in as the user you assigned the role to.
- On the top right corner, Click on your profile and select the ellipsis (...) to see more links. Then click on `Permissions`. You'll find the roles that you've been assigned and the scope.
- Verify that they can view all the resource groups in the specified subscription.
- Verify that the user can not see any resources within the resource groups.
- Verify that they can create support requests;
    - Navigate to the Azure portal.
    - Search for `Help` and click on `Create a support request`.
    - Follow the steps to create a support request.
- On a given scope (subscription, resource group, or resource), Click on `Access control (IAM)` and navigate to the `Role assignments` tab to see the role assignments.
- Using `activity logs`, you can track various actions performed regarding RBAC.

---

## Conclusion

Role-Based Access Control (RBAC) is a powerful tool for managing user permissions and access on Azure resources. By creating custom role definitions and assigning them to users, you can tailor access to meet specific requirements, ensuring security and compliance in your Azure environment.

Management groups provide a hierarchical structure for managing access, policies, and compliance across multiple subscriptions. By organizing your resources into management groups, you can apply access controls, policies, and budgets at different levels of the hierarchy, ensuring consistent governance across your Azure environment.

---

## References and Further Reading

- [Azure RBAC Documentation](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
- [Azure built-in roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)
- [Microsoft Entra built-in roles](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference)
- [Understand Azure role assignments](https://learn.microsoft.com/en-us/training/modules/configure-role-based-access-control/10-summary-resources)
- [Azure Management Groups Documentation](https://learn.microsoft.com/en-us/azure/governance/management-groups/overview)