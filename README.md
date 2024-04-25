# Azure Virtual Desktop Custom Image Templates (CIT) Prerequisites

This solution will deploy the prerequisites for AVD Custom Image Templates as described in the following article:

[Use custom image templates to create custom images in Azure Virtual Desktop | Microsoft Learn](https://learn.microsoft.com/en-us/azure/virtual-desktop/create-custom-image-templates)

## Resources

The following resources are deployed with this solution.  The storage account used for storing _scripts_ or other _build artifacts_ is **optional**. If chosen, a container will be created called **artifacts**.

- Azure Compute Gallery
- Resource Providers on the Subscription
- Role Definitions
- Role Assignments
- User-Assigned Managed Identity
- VM Image Definition

**Optional:** 
- Storage Account and _artifacts_ container
- Role Assignment for User-Assigned Managed Identity

## Prerequisites

This solution assumes certain resources have already been deployed to your Azure environment:

Required:

- Subscription
- Virtual Network

## Deployment Options

To deploy this solution, the principal must have Owner privileges on the Azure subscription.

### Azure Portal

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamasten%2FAVD-CIT-Prereqs%2Fmain%2Fsolution.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamasten%2FAVD-CIT-Prereqs%2Fmain%2FuiDefinition.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#blade/Microsoft_Azure_CreateUIDef/CustomDeploymentBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamasten%2FAVD-CIT-Prereqs%2Fmain%2Fsolution.json/uiFormDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2Fjamasten%2FAVD-CIT-Prereqs%2Fmain%2FuiDefinition.json)

### PowerShell

````powershell
New-AzDeployment `
    -Location '<Azure location>' `
    -TemplateFile 'https://raw.githubusercontent.com/jamasten/AVD-CIT-Prereqs/main/solution.json' `
    -Verbose
````

### Azure CLI

````cli
az deployment sub create \
    --location '<Azure location>' \
    --template-uri 'https://raw.githubusercontent.com/jamasten/AVD-CIT-Prereqs/main/solution.json'
````
