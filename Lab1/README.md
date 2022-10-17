# Lab1

The task for Lab1 is to create an ARM template that
- deploys an Azure Storage Account (Free Tier)
- deploys an Azure Web-App (Free Tier)
- uses parameters

## Deployment

Before you can deploy the template you need either the Azure PowerShell or Azure CLI. To start working with Azure CLI, sign in to Azure using the following command:

    az login

Moreover, if you do not have a resource group, you can create one with the following command:

    az group create --name myResourceGroup --location "West Europe"

Now you can deploy the template with the command below. Keep in mind to replace {resource-group-name} with the appropriate resource group.

    az deployment group create --name mydeployment --resource-group {resource-group-name} --template-file azuredeploy.json --parameters azuredeploy.parameters.json

## Personal experience

I used this [Microsoft tutorial](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell) to create the template. Thanks to this tutorial I had no issues except after creating the **App Service plan** through the Azure portal and trying to deploy the template I got an error saying that a validation for a resource failed. The reason was that with the free tier subscription you can only create one **App Service plan** per region. Therefore, after deleting the previous one I had no problems deploying the template.
