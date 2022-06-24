# Module Structure - Guidelines

A module is a container for multiple resources that are used together. The `.tf` files in your working directory when you run `terraform plan` or `terraform apply` together form the root module. That module may call other modules and connect them together by passing output values from one to input values of another.

Each module is typically located in its own repository in the `terraform-ibm-modules` organization. This enables each modules to have its own release lifecycle. Nested modules may be located within the repostory structure.

The following [template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template) contains a complete and current structure. Use the template to create a repository for new modules.

A complete example of a module following the standard structure is shown below.

```
├── .github/
│   ├── workflows/
│   │   ├── workflow_file1.yml
│   │   ├── .../
├── common-dev-assets -> git submodule on https://github.com/terraform-ibm-modules/common-dev-assets
├── README.md
├── versions.tf
├── variables.tf
├── main.tf
├── outputs.tf
├── module.yaml
├── Makefile
├── .pre-commit-config.yaml
├── modules/
│   ├── nestedA/
│   │   ├── README.md
│   │   ├── variables.tf
│   │   ├── main.tf
│   │   ├── outputs.tf
│   ├── nestedB/
│   ├── .../
├── examples/
│   ├── exampleA/
│   │   ├── main.tf
│   ├── exampleB/
│   ├── .../
├── LICENSE
├── CONTRIBUTING.md
├── CHANGELOG.md
├── test/
│   ├── test_file1.go/
│   ├── .../

```