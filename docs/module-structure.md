# Module structure

A module is a container for multiple resources that are used together. Each module is typically located in its own repository in the `terraform-ibm-modules` organization. This placement enables each module to have its own release lifecycle.

A module might call other modules and connect them by passing output values from one module to input values of another. The repository might also include nested modules in a `modules` directory.

The following structure describes the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template). Use the template to create a repository for new modules. The structure is based on the guidelines from Hashicorp.

```text
├── .github/
│   ├── workflows/
│   │   ├── workflow_file1.yml
│   │   ├── .../
├── common-dev-assets -> git submodule at https://github.com/terraform-ibm-modules/common-dev-assets
├── examples/
│   ├── default/
│   │   ├── main.tf
│   │   ├── .../
│   ├── existing-resources/
│   ├── non-default/
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
│   ├── pr_test.go
│   ├── other_test.go
│   ├── .../
├── .gitmodules
├── .pre-commit-config.yaml
├── .release.rc
├── .secrets.baseline
├── Brewfile/ -> symbolic link to common-dev-assets
├── LICENSE
├── Makefile/ -> symbolic link to common-dev-assets
├── README.md
├── catalogValidationValues.json.template
├── ci -> symbolic link to common-dev-assets
├── commitlint.config.js
├── main.tf
├── outputs.tf
├── renovate.json
├── variables.tf
├── version.tf
├── CODE_OF_CONDUCT.md from terraform-ibm-modules/.github
├── CONTRIBUTING.md from terraform-ibm-modules/.github
├── SUPPORT.md from terraform-ibm-modules/.github
```

For more information about module standards, see [Authoring guidelines](implementation-guidelines.md).

For more information about creating or updating a module, see [Contributing a module](contribute-module.md).
