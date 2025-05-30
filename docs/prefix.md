# Prefix in Deployable Architecture

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
