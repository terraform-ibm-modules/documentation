# Deployable Architecture authoring guidelines

## Prefix in Deployable Architecture

The **`prefix`** input variable allows you to prepend a custom string to the names of all resources created by this automation. This is especially useful for:

- **Avoiding naming collisions** when deploying the same solution multiple times within the same account.
- **Creating identical infrastructure** across multiple regions or environments.
- **Improving resource traceability** by embedding environment or region identifiers into resource names.

If you do not wish to use a prefix, you may set the value to `null` or an empty string (`""`).

**Important**: The automation automatically inserts a hyphen between the prefix and the resource name. Therefore, you do not need to include a hyphen in the prefix yourself.

### Examples

Here are some common patterns for using the prefix:

- **Environment-based**:
  - `dev`, `test`, `prod`
- **Environment + Region**:
  - `dev-eu-gb`, `prod-us-south`, `test-jp-tok`
- **Project-specific**:
  - `webapp-dev`, `ml-prod`, `iot-test`
- **Team or department identifiers**:
  - `fin-dev`, `hr-prod`, `eng-test`
- **Date or version-based** (for temporary or experimental deployments):
  - `exp-202505`, `v2-dev`

These conventions help ensure that resources are clearly grouped and easily identifiable, especially in shared or multi-tenant accounts.

### Naming Rules

To ensure compatibility and consistency, the prefix must follow these rules:

- Must begin with a **lowercase letter**
- May contain only **lowercase letters**, **digits**, and **hyphens (`-`)**
- Must **not end** with a hyphen (`-`)
- Must **not contain consecutive hyphens** (`--`)
- Maximum length: **16 characters**

Here is the code snippet for your reference.

```hcl
variable "prefix" {
  type        = string
  nullable    = true
  description = "The prefix to be added to all resources created by this solution. To skip using a prefix, set this value to null or an empty string. The prefix must begin with a lowercase letter and may contain only lowercase letters, digits, and hyphens '-'. It should not exceed 16 characters, must not end with a hyphen('-'), and can not contain consecutive hyphens ('--'). Example: prod-0205-cos."

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
    condition = length(var.prefix) <= 16
    error_message = "Prefix must not exceed 16 characters."
  }
}
```