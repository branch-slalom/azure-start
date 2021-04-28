# Azure START - 001 - Deploy an Azure App Service
This quickstart shows you how to use an Azure Resource Manager template (ARM template) to deploy an Ubuntu Linux virtual machine (VM) in Azure.

[![Deploy to Azure](https://docs.microsoft.com/en-us/azure/media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2Fbranch-slalom%2Fazure-start%2Fmain%2Fstart001%2F1-deploy-app-service-basic.json)

## Prerequisites

If you don\'t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## 1. ARM Templates Basics

### Deploy the template

1. Select the following image to sign in to Azure and open a template. The template creates a key vault and a secret.

2. Select or enter the following values. Use the default values, when available.

    - **Subscription**: select an Azure subscription.
    - **Resource group**: select an existing resource group from the drop-down, or select **Create new**, enter a unique name for the resource group, and then click **OK**.
    - **Location**: select a location. For example, **Canada Central**.
3. Select **Review + create**. After validation completes, select **Create** to create and deploy the VM.

### Review deployed resources

You can use the Azure portal to check on the VM and other resource that were created. After the deployment is finished, select **Go to resource group** to see the VM and other resources.

## 2. ARM Templates Extra

1. Extend the ARM Template
    a) Add application settings to the Azure App Service using the ARM template
    b) Tag the App Service and the Web App with tags to label the resources with the:
        * Office / Build Center
        * Practice Area
        * Project Code
    c) Complete the ARM template output to display the deployed Azure App Service Url

2. Redeploy the ARM Template
	i) Redeploy the template from the Portal in the 'Custom Deployment' blade

	ii) Redeploy the template using the Azure CLI
```
resourceGroupName=start-test-rg2
deploymentName=2-deploy-app-service-extra # It's good practice to have this unique to identify each deployment separately for auditing
az account set -s '<Subscription Name>'
az deployment group create \
    --name=$deploymentName \
    --resource-group $resourceGroupName \
    --template-file start001/2-deploy-app-service-extra.json \
    --mode Complete
az deployment group show \
    --name=$deploymentName \
    --resource-group $resourceGroupName \
    --filter "properties.outputs" \
    --output table
```

Note: You can monitor your deployment by navigating to the "Resource Group" and under the "Deployments" blade

## 3. Clean up resources

### Using the Portal

When no longer needed, delete the resource group, which deletes the VM and all of the resources in the resource group. 

1. Select the **Resource group**.
2. On the page for the resource group, select **Delete**.
3. When prompted, type the name of the resource group and then select **Delete**.

## Reference
This tutorial was largely inspired from the Microsoft Docs, "[Quickstart: Create an Ubuntu Linux virtual machine using an ARM template](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-template)".