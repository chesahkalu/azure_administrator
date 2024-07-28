# Azure Compliance and Governance Using Tags

This tutorial is designed to empower you to navigate and apply Azure's governance framework effectively, ensuring your resources are organized and compliant using tagging and policies.

---

## Table of Contents

- [Introduction](#introduction)
- [Embracing Management Groups](#embracing-management-groups)
- [Azure Tags](#azure-tags)
- [Task 1: Tagging Resources for Clarity and Management](#task-1-tagging-resources-for-clarity-and-management)
- [Azure Policy](#azure-policy)
- [Task 2: Automating Compliance with Azure Policy](#task-2-automating-compliance-with-azure-policy)
- [Task 3: Streamlining Tag Application with Policy](#task-3-streamlining-tag-application-with-policy)
- [Wrapping Up](#wrapping-up)
- [Further Reading](#further-reading)

---

## Introduction

Azure's governance tools are essential for managing and securing your cloud resources effectively.
This comprehensive guide walks you through the nuances of policy creation, compliance management, resource tagging, and the strategic implementation of management groups.

---

## Azure Tags

- Azure tags are `key-value` pairs that help you organize resources and manage billing. Tags can be applied to resources, resource groups, and subscriptions. They are useful for tracking costs, managing access, enforcing compliance or simply specifying the purpose of a resource.

- They do this by providing metadata that can be used to categorize resources, track costs, and enforce policies. Tags can be used to group resources together, track costs, and enforce policies, by implementing Azure policies to resources based on their tags.

- Tags are `not inherited` by default, but you can use Azure Policy to enforce and inherit tagging requirements(from `resource groups`, `subscriptions`) and automate tag application. This ensures that all resources are tagged consistently and accurately if they are missing tags, and need to inherit tags from their parent resource group.

- Each resource, resource group, and subscription can have a maximum of `50` tag name-value pairs. If you need to apply more tags than the maximum allowed number, use a JSON string for the tag value.

- Tags can be applied from the scope of a `resource`, `resource group`, `subscription`, or `management group`. Tags can be used to categorize resources, track costs, and enforce policies. Tags can be used to group resources together, track costs, and enforce policies, by implementing Azure policies to resources based on their tags.


### Task 1: Tagging Resources for Clarity and Management

Resource tagging facilitates easier management and billing transparency. Follow these steps to implement tagging effectively:

#### 1. **Identify Your Target Resource Group:**
- Access the Azure Portal.
- Locate a resource group for tagging, such as the Cloud Shell resource group.

#### 2. **Apply Your Tag:**
- Navigate to the `Tags` tab within the resource group.
- Add your tag, e.g., `Project:Compliance`.

#### 3. **Confirm Tag Application:**
- Ensure the tag hasn’t been applied to non-designated resources within the group.

---

## Azure Policy

- `Azure Policy` is a service in Azure that you use to create, assign, and manage policies. These policies enforce different rules and effects over your resources, so those resources stay compliant with your corporate standards and service level agreements.

- Enable `built-in policies`, or build `custom policies` for all resource types. Support real-time policy evaluation and enforcement, and periodic or on-demand compliance evaluation.

- Policy assignment can start from the  `management group level`, `subscription level`, or `resource group level`. Policies are inherited by child resources, and you can exclude specific resources from policy enforcement.

- `A policy definition` expresses what to evaluate and what action to take. It describes the `compliance` conditions for a resource, and the actions to complete when the conditions are met. One or more policy definitions are grouped into an `initiative definition`, to control the scope of your policies and evaluate the compliance of your resources. For example, you can ensure all resources in your subscription are tagged, or that virtual machines are encrypted.
There are four basic steps to create and work with policy definitions in Azure Policy: 
  1. `Create a policy definition`: Define what to evaluate and what action to take when the conditions are met, either `custom` or `built-in` policy definitions. `Eg 1`. Require a tag and its value on resources. `Eg 2`. You can create a policy definition to prevent VMs in your organization from being deployed, if they're exposed to a public IP address.

  2. `Create an initiative definition`: Group multiple policy definitions to simplify management and assignment, either `custom` or `built-in` policy definitions. `Eg 1`. You can group policy definitions that enforce tagging, naming conventions, and resource location into a single initiative. `Eg 2`. You can group policy definitions that enforce security settings for a specific service into a single initiative.

  3. `Scope the initiative definition``-``Assingment`: Define the scope of the initiative definition to either limit or specify where it's enforced. `Eg 1`. You can scope an initiative definition to a management group, subscription, or resource group. `Eg 2`. You can scope an initiative definition to a specific resource type, location, or tag.

  4. `Determine compliance`: After you've assigned the initiative definition, you can view the compliance state of your resources. `Eg 1`. You can view the compliance state of all resources in a subscription. `Eg 2`. You can view the compliance state of all resources in a resource group.

---

### Task 2: Automating Compliance with Azure Policy

Enforce tagging consistently across your resources using Azure policies to ensure compliance and governance. Follow these steps to automate compliance:

#### 1. **Explore Policy Options:**
- In the Azure Portal, go to the `Policies` section.
- Find and review the "Require a tag and its value on resources" policy.

#### 2. **Policy Assignment:**
- Apply this policy to your resource group to enforce the `Project:Compliance` tag.

#### 3. **Verify Policy Effectiveness:**
- Test the policy by trying to create a resource without the required tag. The creation should be blocked.

---

### Task 3: Streamlining Tag Application with Policy

Automate the tag application process to ensure compliance and minimize manual efforts.


#### 1. **Policy Assignment for Tag Inheritance:**
- Use the "Inherit a tag from the resource group if missing" policy to automate tag application to new resources.

#### 2. **Setting Up Remediation:**
- Implement a remediation task for the policy to apply it retrospectively.  

#### 3. **Confirming Automated Tagging:**
- Verify that a new resource automatically inherits the `Project:Compliance` tag.

---

## Locks

- Azure provides two types of locks to prevent accidental deletion or modification of resources: `Delete Lock` and `Read-only Lock`.

- A `Delete Lock` prevents the deletion of a resource. It can be removed only by a user with the appropriate permissions. This lock is useful when you want to prevent accidental deletion of a resource. It is applied at the resource level, `but the object can still be modified`.

- A `Read-only Lock` prevents all modifications to a resource. This includes deleting the resource, but also any modifications to the resource's properties.

- To apply a lock to a resource, navigate to the resource in the Azure portal, click on `Locks` under `Settings`, and then click on `+ Add`.

- Choose the type of lock you want to apply, provide a name and a description, and then click `OK`.

- Locks are applied to most Azure resources, and resource level restrictions can be applied to prevent accidental deletion or modification. Locks can then be applied at the `subscription level`, `resource group level`, or `individual resource level`.

- When you apply a lock at a parent scope, all resources within that scope inherit the lock. Even resources created after the lock is applied inherit the loc. 

- If two locks are applied to a resource, the most restrictive lock takes precedence. For example, if a read-only lock is applied to a resource, and a delete lock is applied to a resource group containing that resource, the `read-only` lock takes precedence.


## Wrapping Up

Implementing these strategies will enhance your resource management and governance in Azure. Embrace these practices for an organized, compliant, and efficient cloud environment.

___

## Further Reading

- [Azure Policy Documentation](https://learn.microsoft.com/en-us/azure/governance/policy/overview)
- [Azure Management Groups Overview](https://learn.microsoft.com/en-us/azure/governance/management-groups/overview)
- [Azure Resource Tagging Best Practices](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/tag-resources)
- [Azure Compliance Documentation](https://learn.microsoft.com/en-us/training/modules/describe-features-tools-azure-for-governance-compliance/)
- [Azure Governance Best Practices](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/resources/tools-templates)
- [Interactive Lab: Manage Governance via Azure Polic ](https://learn.microsoft.com/en-us/training/modules/configure-azure-policy/9-simulation-policy)

---