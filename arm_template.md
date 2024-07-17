# Extract an Azure Resource Manager (ARM) Template from an Existing Resource

This guides you through the process of generating an ARM template from an existing Azure resource on the Azure portal. This method allows for the deployment of new resources with similar configurations, streamlining your Azure infrastructure management and `resource provisioning`.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Overview of ARM Templates](#overview-of-arm-templates)
- [Steps to Generate ARM Template](#steps-to-generate-arm-template)
- [Steps to Deploy ARM Template](#steps-to-deploy-arm-template)
- [Conclusion](#conclusion)
- [References and Further Reading](#references-and-further-reading)

---

## Prerequisites

- An understanding of Azure fundamentals.
- An active Azure subscription. [Sign up for a free tier here](https://azure.microsoft.com/en-us/free/).
- Programming Knowledge : An understanding of JSON is required to work with ARM templates.

---

## Overview of ARM Templates

ARM templates are JSON files that define the resources you need to deploy for your Azure solution. Here's a basic structure of an ARM template:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {},
    "functions": [],
    "resources": [],
    "outputs": {}
}
```
- `$schema`: The URL of the schema file that describes the version of the template language.
- `contentVersion`: The version number of the template content for management and tracking purposes.
- `parameters`: Values that are provided when the deployment is executed to customize the deployment.
- `variables`: Values that are used as JSON fragments in the template to simplify template language expressions.
- `functions`: User-defined functions that are available to the template.
- `resources`: The resources to deploy or update.
- `outputs`: Values that are returned after deployment.

### Biceps

Bicep is an alternative DSL (Domain Specific Language) for ARM templates, aiming to simplify the authoring experience. Bicep files are transpiled to ARM JSON templates, making them a powerful and easier-to-read option for managing Azure resources.

---

## Steps to Generate ARM Template

1. Navigate to your resource group in the Azure portal and select `Deployments` from the left-hand menu under `Settings`.
2. Select the deployed resource you want to generate the ARM template for.
3. Click `Template` on the left-hand menu to view the ARM template.
4. On the top, click `Download` to save a compressed file of the Template and Parameters file to your local machine.
5. Extract the file to get the `Template.json` and `Parameters.json` files.

---

## Steps to Deploy ARM Template

1. On the portal search box, type `Deploy a Custom Template`.
2. On custom deployment page click on `Build your own template in the editor`.
3. Edit the template as needed by copying the `Template.json` file in your local machine or upload the file by clicking on `Load file`.
4. Click `Save` and then click `Edit Parameters` to provide the values for the parameters.
5. Edit the parameters as needed by copying the `Parameters.json` file in your local maching or upload the file by clicking on `Load file`.
6. Click `Save` , adjust other details on `Custom Deployment` page and then click `Review + Create`.
7. Review the details and click `Create` to deploy the resources.

---

## Conclusion

Generating ARM templates from existing resources is a powerful way to automate the deployment of Azure resources. By following the steps outlined in this guide, you can streamline your Azure infrastructure management and ensure consistency across your deployments.

---

## References and Further Reading
- [Azure Resource Manager documentation](https://docs.microsoft.com/en-us/azure/azure-resource-manager/)
- [Quickstart templates for Azure deployments](https://learn.microsoft.com/en-us/samples/browse/?expanded=azure&products=azure-resource-manager)
- [GitHub repository of Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates)
- [Create & deploy template - Azure Resource Manager](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell)