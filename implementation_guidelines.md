# IBM Cloud Terraform Modules - Implementation Guidelines

## Module structure

A common [module structure](module_structure.md) is available. Any new module should adhere with this structure. These guidelines are broadly based on the ones prescribed by Hashicorp.

## Module namimg

Module repositories for IBM Cloud must use the three-part name format `terraform-ibm-<NAME>`, where:
- `<NAME>` reflects the type of infrastructure the module manages.
- Use hyphens in the `<NAME>` as delimiter for names with multiple strings. e.g: activity-tracker.

- Module repositories must have a short one-line description of the primary module in the repository

Module repository can have nested modules:
- When naming the nested modules, do not repeat the name of the top level module.
- For example, for a top level module named `terraform-ibm-cos`, do not name the nested module `cos-instance` (since, it will translate to "cos_cos-instance" in the module registry);  instead, use `instance` (to register the child-module as "cos_instance").

## Module documentation

Module documentation should be located in the `README.md` file at the same level as the `main.tf` file for each of the modules in a repository, including the example modules. Additional documentation may be located in a sub directory named `docs`.

For consistency across modules, all `README.md` files should follow the same structure. See the [README.md template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/README.md).

# Module variables

## Variable naming:

Input and output variable name must correspond to the names used in the IBM Cloud UI, CLI, or in the IBM Cloud Documentation.

For common variables, use the standard variable names from the template variable dictionary. Schematics has been collecting a dictionary - See link [TODO]

## Variable description:

Input and output variables should have a short description in the `variables.tf` and in `README.md` file. Description should be full English sentences. Avoid using abbreviations.

Note that the `README.md` file section is automatically generated based on the description in the `variables.tf` file through the terraform doc pre-commit hook (https://github.com/terraform-ibm-modules/common-dev-assets/blob/main/module-assets/.pre-commit-config.yaml#L28). Therefore, module contributors do not need to manually update the variable description in the `README.md` file.

## Variable defaults:

Include defaults wherever possible and the sensitive flag as appropriate. Only update the meaning of a type with agreement of the governance body.

# Module examples

Every module must contain at least one example. An example is a [root terraform module](https://www.terraform.io/language/modules#the-root-module) that utilizes the module, and demonstrate its usage.

The examples are located under the `/examples` directory. See [module structure](module_structure.md).

Once you add an example, do not forget to link it from the README.md file, under the [Examples section](https://github.com/terraform-ibm-modules/terraform-ibm-module-template#examples)


A few recommendations, and good practices:
- Try to have at least one of the example as simple and basic as possible. For instance, calling the module with all default input values. It is common to name this example "basic". 
- Avoid requiring any manual set up as a pre-req to running the example. In an ideal scenario, an example should set up all dependencies programmatically as part of its execution. For instance, the terraform code for an `openshift-vpc-module` would create the vpc that is used then passed as an input to the `openshift-vpc-module`.
- Add as many examples as necessary to cover the most common usage scenarios of your module. Cover one specific usage scenario per example, rather than attempting to cover multiple usage scenarios in the same example. This keeps examples simple to consume and understand.
- Put yourself in the shoes of someone who want to quickly kick the tyres and understand how to consume the module in their own terraform code.


# Module validation tests

Modules must contains at the minumum one automated validation test that apply, destroy and test idempotency of the module. See [test.md](Validation tests) for details.

# Module versioning

[Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) are used to identify module versions. Release tags are based [semantic version](https://semver.org/) guidelines. For example, v1.0.0.

As a module author or contributor, you do not need to manually release new version. When a Pull Request is merged into the main/master branch, a new releases are automatically created by the ` terraform-ibm-modules` release automation, provided that the validation pipeline passes.

The release version is computed based on the type of change made to the module. The type of change is determined by the commit messages, which follows the [Angular Commit Message Convertions](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#-commit-message-format). [semantic-release engine](https://github.com/semantic-release/semantic-release) is used to generate the semantic version and release.