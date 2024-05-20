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
- Storage Account Role Assignment for User-Assigned Managed Identity

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

---
# Deployment Example

The following will provide you a quick walk-through with a deployment.

## Basics

Under **Instance details**:

1. Select the appropriate `Subscription`.
2. Select the appropriate `Region`.
3. Select `Use existing resource group` if applicable.  If not chosen, a resource group will be created for you.
4. Select `Deploy a storage account for build artifiacts` if you need a storage account created to host custom scripts.  The solution will create a container called `artifacts` and set the appropriate permissions for the managed identity.

Under **Resource Names**:

1. Select the name for the `Compute Gallery` that will be created.
2. Select the name for the `Deployment Script` that will be created.  The deployment script is used to help support the deployment of the solution.
3. Select the name for the `Image Definition` that will be created.
4. _If `Deploy a storage account for build artifacts` was selected_, select the name of the `Storage Account` that will be created.
5. Select the name of the `User assigned identity` that will be created.

Click **Next**.

## Networking

1. Select `Enable custom virtual network`.  This is to setup the Virtual Network setup for AIB/CIT Build VMs.
2. Select the `Virtual Network`.
3. Select the `Subnet`.

Click **Next**.

## Image Definition

1. If desired, select `Supports network acceleration`.
2. If desired, select `Supports hibernation`.
3. Under `Security Type`, select the appropriate security features for the VM Image Definition.  **NOTE:** Most environments may require `Trusted Launch` if they are deploying the latest versions of Windows.
4. Under `Publisher`, select if you're deploying a `Microsoft Windows Desktop` or `Microsoft Windows Server` Operating System.
5. Under `Offer`, the drop down will differ based on what you chose for `Publisher`.  As an example, if you're targeting a Windows 11 Multi-Session Operating System with M365 Applications, you will want to use `office-365`.
6. Under `SKU`, the drop down will differ based on what you chose for `Offer`.  As an example, if you're targeting a Windows 11 23H2 Multi-Session Operating System with M365 Applications, you will want to use `win11-23h2-avd-m365`.

Click **Next**.

## Tags

Enter the appropriate `Tags` for the environment.

Click **Next**.

## Review + Create

Review the options you have selected and click `Create`.
