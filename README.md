# StorageAccountProvisionAz_Terraform

##Terraform module for creating and managing Azure Storage Account resources

## Examples

```
module "Terraform_Azure_ResourceGroup" {
  source="git::https://github.com/pracip96/Terraform_AzResourceGroup.git"
  
  }

resource "azurerm_storage_account" "example" {
  name                     = var.storageaccname
  resource_group_name      = module.Terraform_Azure_ResourceGroup.az-rg-name
  location                 = "Central US"
  account_tier             = var.account_tier
  account_replication_type = var.account_replication_type

  tags = {
    environmenttag = local.environment
  }
}
resource "azurerm_storage_container" "storageacccontainer" {
  name                  = var.storage_container_name
  storage_account_name  = azurerm_storage_account.storageacc_prasanna.name
  container_access_type = "private"
}
resource "azurerm_storage_blob" "FileOnAzure" {
  name                   = var.azurerm_storage_blob_name
  storage_account_name   = azurerm_storage_account.storageacc_prasanna.name
  storage_container_name = azurerm_storage_container.storageacccontainer.name
  type                   = "Block"
  source                 = "FileonAzure.txt"
}
```

## Requirements

| Name | Version |
| --- | --- |
| terraform | = 1.4.6 |

## Providers

| Name | Version |
| --- | --- |
| azurerm | >= 3.54 |

## Inputs

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| storageaccname | The Name of the storageaccount | `string` | yes |
| account_tier | Defines the Tier to use for this storage account. Valid options are Standard and Premium | `string` | yes |
| account_replication_type | Defines the type of replication to use for storage account. Valid options are LRS, GRS, RAGRS, ZRS, GZRS and RAGZRS | `string` | yes |
| storage_container_name | The name of the Container which should be created within the Storage Account | `string` | yes |
| azurerm_storage_blob_name | The name of the storage blob. Must be unique within the storage container the blob is located | `string` | yes |


## Help

**Got a question?**

(https://registry.terraform.io/providers/hashicorp/azurerm/latest).




