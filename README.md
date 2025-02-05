# Azure-AZ204-Lab1
Azure AZ 204 Lab 01: Building a web application on Azure

## Instructions

### 1. Setup Azure Storage

To create the storage account the following commands where used.

```bash
az login --tenant <tenant-id>
az group create --location <location name> --name <resource group name>
az storage account create --name <storage account name>  --resource-group <resource group name> --sku Standard_LRS
az storage account show-connection-string --name <storage account name> -g <resource group name>
az storage container create --name az204bloblab1 --connection-string <storage account connection string> --resource-group <resource group name>
az storage blob upload --connection-string <connection string> --container-name <name> --file <file path>
```

Whe the account is created, one can specify the following:

```
[--access-tier {Cold, Cool, Hot, Premium}]
[--kind {BlobStorage, BlockBlobStorage, FileStorage, Storage, StorageV2}]
[--public-network-access {Disabled, Enabled, SecuredByPerimeter}]
```

### 2. Setup Back End and Front End Web Apps

To create the web apps using the Azure CLI, the following commands were used:

```bash
az appservice plan create -g <resource group name> --name <plan name> --sku FREE
az webapp list-runtimes
az webapp create --name <web app name> --plan <plan name> --resource-group <resource group name> --runtime dotnet:8
az webapp config appsettings set --name <web app name> --resource-group <resource group name> --settings StorageConnectionString="<connection-string>"
az webapp config appsettings set --resource-group <resource group name> --name <web app name> --settings ApiUrl="<api url>"
az webapp deploy --resource-group <resource group name> --name <web app name> --src-path <source code zip path> --type zip
```

The appsettings can be deployed using a JSON file with all the related settings. Aditionally, there's an option for DB connection strings directly. The az webapp deployment command was deprecated, so instead the deploy comand was used.
