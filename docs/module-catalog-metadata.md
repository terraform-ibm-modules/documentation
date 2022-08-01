# Metadata that describes a module

?> *DRAFT*: This content is not finalized

The `index.yml` file describes an IBM Cloud Terraform module. The file includes the metadata such as name, description, variables, and dependencies of the module and submodules. Parts of the file are generated.

## Overview of index.yml (Current version)

?> *TODO* Placeholder for description of the yaml file

## Template metadata generator

A template metadata generator tool generates the metadata of the variables from the Terraform logic in a module. The following table describes the variables that are extracted by the tool.

?> *TODO* The metadata generator tool is not yet implemented in the IBM Cloud Terraform modules project.


| Name | Type | Description |
|---|---|---|
| `name` | string | Variable name |
| `type` | string | Data type of the variable |
| `description` | string | Description of the variable |
| `default` | bool | Default value of the variable |
| `required` | bool | Whether the variable is required |
| `sensitive` | bool | Whether the variable contains credentials, secrets, or other sensitive values |
| `aliases` | list(string) | The list of aliases for the variable name |
| `cloud_data_type` | string | The type of IBM Cloud data. Allowable values: `Region`, `ResourceInstance`, `CRN`, `Tags`, `ResourceGroup` |
|`link_status`|string|The status of the link|
| `immutable` | bool | If `true`, altering the value of the variable destroys and re-creates a resource (`ForceNew` behavior) |
| `hidden` | bool | If `true`, the variable is not displayed in the UI or CLI. |
| `options` | list(string) | Allowable values for the variable |
| `min_value` | string | Minimum value of a number variable. Validation is defined in the provider |
| `max_value` | string | Maximum value of number variable. Validation is defined in the provider |
| `min_value_length` | int | The minimum length of a string variable. Validation is defined in the provider. |
| `max_value_length` | int | The maximum length of a string variable. Validation is defined in the provider. |
| `matches` | string | The regular expression (regex) for the variable value. |
| `optional` | bool | Whether the variable is optional (`Optional` behavior) |
| `computed` | bool | Whether the variable is computed or derived (`Computed` behavior) |
| `elem` | provider schema struct | Child arguments of complex variable types |
| `max_items` | int | Maximum number of items for a `list` or `set` variable. Validation is defined in the provider schema. |
| `min_items` | int | Minimum number of items for a list or set variable. Validation is defined in the provider schema. |
| `deprecated` | bool | Whether the variable is deprecated in the provider schema. |
| `cloud_data_range` | string | The range of IBM Cloud data for the `CloudDataType`. For the `ResourceInstance` data type, the format is `["service:", ":"]`. |

You can see an example of the `index.yml` file after the generator tool adds the metadata at https://github.com/kavya498/terraform-ibm-object-storage/blob/gh-pages/index.yaml.


This tool allows viewing variable information in json format

``` json
{
    "variables": {   
        "A": {
            "name": "A",
            "type": "string",
            "default": "A default",
            "optional":true,
            "computed": true,
            "min_length": 1,
            "max_length": 63,
            "matches": "^([a-z]|[a-z][-a-z0-9]*[a-z0-9])$"
        
        },
        "instance_id": {
            "name": "instance_id",
            "type": "string",
            "description": "Id of instance",
            "required":true,
            "immutable": true,
            "cloud_data_type" : "ResourceInstance",
            "cloud_data_range": ["service:kms"]
        }
    }
}
```