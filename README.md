# IBM Cloud - Terraform modules

This repo captures the guidelines to contribute to either existing repo or creating new repo under `terraform-ibm-modules` org. 

## Guidelines

 Meeting the requirements for publishing a repo is extremely easy. The list below contains all the guidelines for publishing a repo or contributing to existing repo. The list may appear long only to ensure we're detailed, but adhering to the requirements should happen naturally.

* `GitHub` The module must be on GitHub and must be a public repo.

* `Repository Name` terraform-<PROVIDER>-<NAME>. Module repositories must use this three-part name format, where <NAME> reflects the type of infrastructure the module manages and <PROVIDER> is the main provider where it creates that infrastructure. The <NAME> segment can contain additional hyphens. 

* `Repository description` The GitHub repository description is used to populate the short description of the module. This should be a simple one sentence description of the module.

* `Release tags` - Tags are used to identify module versions. Release tag names must be a semantic version, which can optionally be prefixed with a v. For example, v1.0.0.

* `Module structure` The module must adhere to the standard module structure. For more details, read the [document here](module_structure.md).

* `Module inputs` - Make sure that name of input varaibles are inline with respective UI page input varaibles. This is to make the user feel same while provisioining the resource either through terraform module or UI. Input Variables should have descriptions.  Use `input.tfvars` file to configue any complex type constraints like list, map etc. For more information, read the [guidelines here](input_variables.md). 

* `Optional input arguments` - Make sure the module includes both mandatory and optional arguments, by doing this we enable user to configure the resource as he wishes. For the optional arguments, have a conditional check and send the default value, if the user input is absent.  

* `Module outputs` - Use to return results to the calling module, which it can then use to populate arguments elsewhere. Outputs should have descriptions. For more information, read the [guidelines here](output_values.md). 


    