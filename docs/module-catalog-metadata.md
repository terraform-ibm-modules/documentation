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
| `secure` | bool | Whether the variable contains credentials, secrets, or other sensitive values |
| `value` | string | Value of the variable |
| `type` | string | Data type of the variable |
| `description` | string | Description of the variable |
| `source` | string | Source identifier of the module in the form `.` |
| `attributeName` | string | Name of the argument in the module block that the variable is mapped to. When the value is part of the Terraform meta-arguments such as `count`, ignore data that is related to the provider. |
| `required | bool | Whether the variable is required |
| `default | bool | Default value of the variable |
| `computed` | bool | Whether the variable is computed or derived (`Computed` behavior) |
| `elem` | provider schema struct | Child arguments of complex variable types |
| `immutable` | bool | If `true`, altering the value of the variable destroys and re-creates a resource (`ForceNew` behavior) |
| `maxItems` | int | Maximum number of items for a `list` or `set` variable. Validation is defined in the provider schema. |
| `minItems` | int | Minimum number of items for a list or set variable. Validation is defined in the provider schema. |
| `deprecated` | bool | Whether the variable is deprecated in the provider schema. |
| `minValue` | string | Minimum value of a number variable. Validation is defined in the provider |
| `maxValue` | string | Maximum value of number variable. Validation is defined in the provider |
| `options` | list(string) | Allowable values for the variable |
| `matches` | string | The regular expression (regex) for the variable value. |
| `minValueLength` | int | The minimum length of a string variable. Validation is defined in the provider. |
| `maxValueLength` | int | The maximum length of a string variable. Validation is defined in the provider. |
| `CloudDataType` | string | The type of IBM Cloud data. Allowable values: `Region`, `ResourceInstance`, `CRN`, `Tags`, `ResourceGroup` |
| `CloudDataRange` | string | The range of IBM Cloud data for the `CloudDataType`. For the `ResourceInstance` data type, the format is `["service:", ":"]`. |
| `aliases` | list(string) | The list of aliases for the variable name |
| `hidden` | bool | If `true`, the variable is not displayed in the UI or CLI. |
| `position` | int | The relative position of the variable in a list |
| `groupBy` | string | The way to group variables: by services, resource, or data sources. |

You can see an example of the `index.yml` file after the generator tool adds the metadata at https://github.com/kavya498/terraform-ibm-object-storage/blob/gh-pages/index.yaml.
