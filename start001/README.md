# Azure START - 001 - Deploy an Ubuntu VM
This quickstart shows you how to use an Azure Resource Manager template (ARM template) to deploy an Ubuntu Linux virtual machine (VM) in Azure.

[![Deploy to Azure](https://docs.microsoft.com/en-us/azure/media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2f101-vm-simple-linux%2fazuredeploy.json)

## Prerequisites

If you don\'t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## 1. ARM Templates Basics

### Deploy the template

1. Select the following image to sign in to Azure and open a template. The template creates a key vault and a secret.

2. Select or enter the following values. Use the default values, when available.

    - **Subscription**: select an Azure subscription.
    - **Resource group**: select an existing resource group from the drop-down, or select **Create new**, enter a unique name for the resource group, and then click **OK**.
    - **Location**: select a location.  For example, **Central US**.
    - **Admin username**: provide a username, such as *azureuser*.
    - **Authentication type**: You can choose between using an SSH key or a password.
    - **Admin Password Or Key** depending on what you choose for authentication type:
        - If you choose **password**, the password must be at least 12 characters long and meet the [defined complexity requirements](faq.md#what-are-the-password-requirements-when-creating-a-vm).
        - If you choose **sshPublicKey**, paste in the contents of your public key.
    - **DNS label prefix**: enter a unique identifier to use as part of the DNS label.
    - **Ubuntu OS version**: select which version of Ubuntu you want to run on the VM.
    - **Location**: the default is the same location as the resource group, if it already exists.
    - **VM size**: select the [size](../sizes.md) to use for the VM.
    - **Virtual Network Name**: name to be used for the vNet.
    - **Subnet Name**: name for the subnet the VM should use.
    - **Network Security Group Name**: name for the NSG.
1. Select **Review + create**. After validation completes, select **Create** to create and deploy the VM.


The Azure portal is used to deploy the template. In addition to the Azure portal, you can also use the Azure CLI, Azure PowerShell, and REST API. To learn other deployment methods, see [Deploy templates](../../azure-resource-manager/templates/deploy-cli.md).

### Review deployed resources

You can use the Azure portal to check on the VM and other resource that were created. After the deployment is finished, select **Go to resource group** to see the VM and other resources.

## 2. ARM Templates Extra
1. Create a new ARM template to organize the resources in multiple resource groups

## 3. Clean up resources

### Using the Portal

When no longer needed, delete the resource group, which deletes the VM and all of the resources in the resource group. 

1. Select the **Resource group**.
1. On the page for the resource group, select **Delete**.
1. When prompted, type the name of the resource group and then select **Delete**.

### With the Azure CLI


## Reference
This tutorial was largely inspired from the Microsoft Docs, "[Quickstart: Create an Ubuntu Linux virtual machine using an ARM template](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-template)".