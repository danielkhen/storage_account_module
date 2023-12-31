<!-- BEGIN_TF_DOCS -->

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_access_tier"></a> [access\_tier](#input\_access\_tier) | (Optional) The access tier of the storage account. | `string` | `"Hot"` | no |
| <a name="input_account_kind"></a> [account\_kind](#input\_account\_kind) | (Optional) The kind of the storage account. | `string` | `"StorageV2"` | no |
| <a name="input_account_replication_type"></a> [account\_replication\_type](#input\_account\_replication\_type) | (Required) The type of replication used for this storage account. | `string` | n/a | yes |
| <a name="input_account_tier"></a> [account\_tier](#input\_account\_tier) | (Required) The tier of the storage account. | `string` | n/a | yes |
| <a name="input_enable_https_traffic_only"></a> [enable\_https\_traffic\_only](#input\_enable\_https\_traffic\_only) | (Optional) Use only https traffic. | `bool` | `true` | no |
| <a name="input_location"></a> [location](#input\_location) | (Required) The location of the storage account. | `string` | n/a | yes |
| <a name="input_log_analytics_id"></a> [log\_analytics\_id](#input\_log\_analytics\_id) | (Required) The id of the log analytics workspace. | `string` | n/a | yes |
| <a name="input_name"></a> [name](#input\_name) | (Required) The name of the storage account. | `string` | n/a | yes |
| <a name="input_private_dns_enabled"></a> [private\_dns\_enabled](#input\_private\_dns\_enabled) | (Optional) Should the private endpoint be attached to a private dns zone. | `bool` | `false` | no |
| <a name="input_private_endpoint_enabled"></a> [private\_endpoint\_enabled](#input\_private\_endpoint\_enabled) | (Optional) Should the container registry have a private endpoint. | `bool` | `false` | no |
| <a name="input_private_endpoints"></a> [private\_endpoints](#input\_private\_endpoints) | (Optional) A list of private endpoints of the storage subresources. | <pre>list(object({<br>    name             = string<br>    subresource_name = string<br>    dns_name         = optional(string)<br>  }))</pre> | `[]` | no |
| <a name="input_private_endpoints_subnet_id"></a> [private\_endpoints\_subnet\_id](#input\_private\_endpoints\_subnet\_id) | (Optional) The subnet id of the private endpoints. | `string` | `false` | no |
| <a name="input_resource_group_name"></a> [resource\_group\_name](#input\_resource\_group\_name) | (Required) The resource group name of the storage account. | `string` | n/a | yes |
| <a name="input_vnet_links"></a> [vnet\_links](#input\_vnet\_links) | (Optional) A list of virtual networks to link with the private dns zone. | <pre>list(object({<br>    name    = string<br>    vnet_id = string<br>  }))</pre> | `[]` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_id"></a> [id](#output\_id) | The id of the storage account. |
| <a name="output_name"></a> [name](#output\_name) | The name of the storage account. |
| <a name="output_object"></a> [object](#output\_object) | The storage account object. |

## Resources

| Name | Type |
|------|------|
| [azurerm_storage_account.storage](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/storage_account) | resource |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_private_dns_zone"></a> [private\_dns\_zone](#module\_private\_dns\_zone) | github.com/danielkhen/private_dns_zone_module | n/a |
| <a name="module_storage_diagnostic"></a> [storage\_diagnostic](#module\_storage\_diagnostic) | github.com/danielkhen/diagnostic_setting_module | n/a |
| <a name="module_subresources_diagnostics"></a> [subresources\_diagnostics](#module\_subresources\_diagnostics) | github.com/danielkhen/diagnostic_setting_module | n/a |
| <a name="module_subresources_private_endpoints"></a> [subresources\_private\_endpoints](#module\_subresources\_private\_endpoints) | github.com/danielkhen/private_endpoint_module | n/a |

## Example Code

```hcl
module "storage_account" {
  source = "github.com/danielkhen/storage_account_module"

  name                          = "example-storage"
  location                      = "westeurope"
  resource_group_name           = azurerm_resource_group.example.name
  account_tier                  = "Standard"
  account_replication_type      = "LRS"
  account_kind                  = "BlobStorage"
  enable_https_traffic_only     = true
  access_tier                   = "Hot"
  public_network_access_enabled = false
  log_analytics_id              = azurerm_log_analytics_workspace.example.id
}
```
<!-- END_TF_DOCS -->