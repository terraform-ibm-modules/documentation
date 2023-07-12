# Module structure

A module is a container for multiple resources that are used together. Each module is typically located in its own repository in the `terraform-ibm-modules` organization. This placement enables each module to have its own release lifecycle.

A module might call other modules and connect them by passing output values from one module to input values of another. The repository might also include nested modules (submodules that are not at the root level).

?> **Tip**: Organize nested modules in the `modules/` directory. For more information about module structure, see [standard module structure](https://developer.hashicorp.com/terraform/language/modules/develop/structure) in the Hashicorp docs.

The following structure describes the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template). Use the template to create a repository for new modules. The structure is based on the guidelines from Hashicorp.

```text
├── .github/
│   ├── workflows/
│   │   ├── workflow_file1.yml
│   │   ├── .../
├── common-dev-assets -> git submodule at https://github.com/terraform-ibm-modules/common-dev-assets
├── examples/
│   ├── basic/
│   │   ├── main.tf
│   │   ├── .../
│   ├── complete/
│   ├── .../
├── modules/
│   ├── nestedA/
│   │   ├── README.md
│   │   ├── variables.tf
│   │   ├── main.tf
│   │   ├── outputs.tf
│   ├── nestedB/
│   ├── .../
├── reference-architectures/
│   ├── architecture-example.md
│   ├── example-architecture-diagram.svg
├── tests/
│   ├── go.mod
│   ├── go.sum
│   ├── pr_test.go
│   ├── other_test.go
│   ├── .../
├── .gitmodules
├── .pre-commit-config.yaml
├── .releaserc
├── .secrets.baseline
├── LICENSE
├── Makefile/ -> symbolic link to common-dev-assets
├── README.md
├── ci -> symbolic link to common-dev-assets
├── commitlint.config.js
├── cra-config.yaml
├── cra-tf-validate-ignore-rules.json
├── module-metadata.json
├── main.tf
├── outputs.tf
├── renovate.json
├── variables.tf
├── version.tf
├── CODE_OF_CONDUCT.md from terraform-ibm-modules/.github
├── CONTRIBUTING.md from terraform-ibm-modules/.github
├── SUPPORT.md from terraform-ibm-modules/.github
```

## For more information

- For more information about module standards, see [Authoring guidelines](implementation-guidelines.md).
- For more information about creating or updating a module, see [Contributing a module](contribute-module.md).
