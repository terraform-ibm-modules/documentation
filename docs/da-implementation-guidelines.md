# Deployable Architecture authoring guidelines

Below you will find some guidance on best practises that should be used when authoring a new Deployable Architecture (DA). In addition, there is some common guidance available in the following links:
- [Best practices for creating deployable architectures](https://cloud.ibm.com/docs/secure-enterprise?topic=secure-enterprise-best-practice-deployable-arch)
- [Best practices for Terraform on IBM Cloud](https://cloud.ibm.com/docs/terraform-on-ibm-cloud?topic=terraform-on-ibm-cloud-white-paper#deployable-architecture-overview)

## Prefix

All Deployable Architecture solutions should have an optional **`prefix`** input variable that complies with the following criteria:
- Input should have no default value, but set `nullable = true` to allow user to pass `null` incase they do not wish to use a prefix. This would be for advanced users who may need full control over resource naming.
- Add validation to the variable. See the below code snippet for the recommended validation to be added across all DAs. Ideally all DAs should have the same validation so the `prefix` value is accepted for all DAs for the case where it may be used for input mapping when configuring dependant (add-on) DAs.
- Ensure to include the details of the required format in the variable description, an example value, and link to the helper doc just like what is shown in the code snippet below. This should be consistent across all DAs.
- The prefix variable logic should be handled in a local variable so logic does not have repeated in the terraform code. For example:
  ```hcl
  locals {
    prefix        = var.prefix != null ? trimspace(var.prefix) != "" ? "${var.prefix}-" : "" : ""
    instance_name = "${local.prefix}${var.instance_name}"
  }
  ```
- Ensure that every variable that will use the prefix includes details about the prefix in the variable description. For example:
  ```hcl
  variable "instance_name" {
    type        = string
    default     = "instance"
    description = "The name for the <some service> instance provisioned by this solution. If a prefix input variable is specified, the prefix is added to the name in the `<prefix>-<instance_name>` format."
    nullable    = false
  }
  ```

### Code snippet example
The following code should be used consistently across all DAs (tweak the example value that is included in the description so it is relevant to the DA being created):

```hcl
variable "prefix" {
  type        = string
  nullable    = true
  description = "The prefix to be added to all resources created by this solution. To skip using a prefix, set this value to null or an empty string. The prefix must begin with a lowercase letter and may contain only lowercase letters, digits, and hyphens '-'. It should not exceed 16 characters, must not end with a hyphen('-'), and can not contain consecutive hyphens ('--'). Example: prod-0205-cos. [Learn more](https://terraform-ibm-modules.github.io/documentation/#/prefix.md)."

  validation {
  # - null and empty string is allowed
  # - Must not contain consecutive hyphens (--): length(regexall("--", var.prefix)) == 0
  # - Starts with a lowercase letter: [a-z]
  # - Contains only lowercase letters (a–z), digits (0–9), and hyphens (-) 
  # - Must not end with a hyphen (-): [a-z0-9]
  condition = (var.prefix == null || var.prefix == "" ? true :
    alltrue([
      can(regex("^[a-z][-a-z0-9]*[a-z0-9]$", var.prefix)),
      length(regexall("--", var.prefix)) == 0
    ])
  )
  error_message = "Prefix must begin with a lowercase letter and may contain only lowercase letters, digits, and hyphens '-'. It must not end with a hyphen('-'), and cannot contain consecutive hyphens ('--')."
 }
 
  validation {
   # must not exceed 16 characters in length
    condition = var.prefix == null || var.prefix == "" ? true : length(var.prefix) <= 16
    error_message = "Prefix must not exceed 16 characters."
  }
}
```
