# IBM Cloud Terraform Modules - Implementation Guidelines

The following guidelines MUST be followed for publishing a module in this organization.

## Module structure

Modules must adhere to common structure. See the [module structure](module_structure.md) for details. These guidelines are broadly based on the ones prescribed by Hashicorp.

## Module namimg

Module repositories for IBM Cloud must use the three-part name format `terraform-ibm-<NAME>`, where 
- `<NAME>` reflects the type of infrastructure the module manages.
- Use hyphens in the `<NAME>` as delimiter for names with multiple strings. e.g: activity-tracker.

- Module repositories must have a short one-line description of the primary module in the repository

The module repository can have nested modules:
- While naming the nested modules, do not repeat the name of the top level module.
- For example, for a top level module named terraform-ibm-cos, do not name the sub module as cos-intance (since, it will translate to "cos_cos-instance" in the module registry);  instead, use instance (to register the child-module as "cos_instance").

## Module documentation

Module documentation should be located in the `README.md` file at the same level as the `main.tf` file for each of the modules in a repository. Additional documentation may be located in a folder named docs.

For consistency across modules, all README.md files should follow the same structure. See the [template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/README.md).

# Module variables

Naming:
- Input and output variable name must correspond to the names used in the IBM Cloud UI, CLI or in the Docs. This is to enable the consumer to cross-refer the inputs across terraform modules, UI & CLI.
- For common variables, use the standard variable names from the template variable dictionary. Schematics has been collecting a dictionary - See link https://ibm.ent.box.com/file/804265261223?s=38rv68zvptzz9syvr1a6myjcn3z28tha


Description:
- Input and output variable should have description in the variable.tf and in readme.md file. Note that the readme.md file section is automatically generated based on the data in the variable.tf file through the terradoc pre-commit hook (https://github.com/terraform-ibm-modules/common-dev-assets/blob/main/module-assets/.pre-commit-config.yaml#L28)


Defaults:
- Include defaults wherever possible and the sensitive flag as appropriate. Only update the meaning of a type with agreement of the governance body.

# Module examples

Every module must contain at least one example. An example is a [root terraform module](https://www.terraform.io/language/modules#the-root-module) that utilizes the module, and demonstrate its usage.

The examples are located under the /examples folder. See [Module structure]([module structure](module_structure.md).


A few recommendations, and good practices:
- One of the example should be as simple as possible. It is common to name this example "basic". 
- Avoid requiring any manual set up. In an ideal scenario, the basic example should set up all dependencies programmatically . For example, the code for an openshift-vpc-module would create the vpc that is used then passed as an input to the openshift-vpc-module.
- Add as many examples as necessary to cover the most common usage scenarios of your module. Cover one specific usage scenario per example, rather than attempting to cover multiple usage scenarios in the same example. This keeps examples simple to consume and understand.
- Put yourself in the shoes of someone who want to quickly kick the tires and understand how to consume your module in their terraform code.


# Module validation tests

Modules must contains at the minumum one automated validation test. See [test.md] for details.

# Module versioning

Git tags are used to identify module versions. Release tag names are be a [semantic version](https://semver.org/), which can optionally be prefixed with a v. For example, v1.0.0.

As a module author or contributor, you do not need to manually release new version. New releases are automatically created provided that the validation pipeline passes, when a PR is merged into the main/master branch.

The release version number is computed based on the type of change made to the module. The type of change is determined by the commit messages, which follows the [Angular Commit Message Convertions](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#-commit-message-format). [semantic-release engine](https://github.com/semantic-release/semantic-release) is used to generated the semantic version and release.