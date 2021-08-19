# IBM Cloud Terraform Modules - Implementation Guidelines

The following guidelines MUST be followed for publishing a module in this organization.

* `terraform-ibm-module-template` 
  - Use this [template repo](https://github.com/terraform-ibm-modules/terraform-ibm-module-template) as the starting point to create a new repo module. 

* `Module repository` 
  - Module repositories for IBM Cloud must use the three-part name format `terraform-ibm-<NAME>`, where 
    * `<NAME>` reflects the type of infrastructure the module manages. 
    * Use hyphens in the `<NAME>` as delimiter for names with multiple strings. e.g: activity-tracker.
  - Module repositories must have a short one-line description of the primary module in the repository
  - The module repository can have both `root-module` and `child-modules`
    * While naming the child-modules, do not repeat the name of the root-module.  
    * For example, for a root-module named `terraform-ibm-cos`, do not name the child module as `cos-intance` (since, it will translate to "cos_cos-instance" in the module registry);  instead, use `instance` (to register the child-module as "cos_instance"). 
  - Other files in the Module repository
    * `.gitignore` -  to specify intentionally the untracked files that Git should ignore.
    * `.pre-commit-config.yaml` - to identify simple issues before submission to code review. The pre-commit hooks will record issues in code, such as missing semicolons, trailing whitespace, and debug statements. 

* `Module structure` 
  - MUST adhere to the [module structure](module_structure.md) prescribed by Hashicorp.

* `Module inputs` 
  - Module inputs are used to configure the resources. The module inputs are either _mandatory_ or _optional_
    * _Optional_ input variable must use the _default value_, if the user-input for the module is absent (or blank).
  - _Input variable_ name must correspond to the names used in the IBM Cloud UI, CLI or in the Docs. This is to enable the consumer to cross-refer the inputs across terraform modules, UI & CLI. 
  - _Input variable_ should have description in the vars.tf and in readme.md file.  
  - Use `input.tfvars` file to configue any complex type constraints like list, map etc. 
  - MUST adhere to the [input variables guidelines](input_variables.md). 

* `Module outputs` 
  - _Output variable_ is used to return results to the calling module. 
  - _Output variables_ should have description in the readme.md file. 
  - MUST adhere to the [output variables guidelines](output_values.md). 

* `Module release tags` 
  - Tags are used to identify module versions. 
  - Release tag names must be a semantic version, which can optionally be prefixed with a v. For example, v1.0.0.

* `Source path` 
  - Use relative path to root-module or child-module, while refering to them within the same repository

* `Github actions`
  - Used to automate the following
    * validate the PR before it gets merged onto main branch. 
    * run the test cases perodically to assure the quality of the modules & exmaples
  - Use `test` directory to write the `terratest` automation for the modules & examples
    * Example [test file](https://github.com/terraform-ibm-modules/terraform-ibm-iam/blob/main/test/access-group/access_group_test.go). 
    * [To run terratest files locally](terratest.md)

