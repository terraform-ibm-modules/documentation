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

* `Naming Modules` When we regiter our module repo ( naming convention `terraform-<PROVIDER>-<NAME>` ) with terraform registry, it picks up the `NAME` from above naming convention and consider it as name of the root module. All the sub-modules will be prefixed with this root module followed by underscore. Hence do not repeat the root module name in sub-module creation.

    E.g: Say we created a module repo called `terraform-ibm-cos` and we have 2 sub-modules named `cos-instance` and `cos_bucket`. Now, when we register our module with terraform registry, it generates module blocks as follows

    ```
    module "cos_cos-instance" {
        source  = "terraform-ibm-modules/cos/ibm//modules/cos-instance"
        version = "1.0.0"
    } 
    ```

    And if we want to name a sub-module with multiple strings, use symbol `-` as delimiter. e.g: activity-tracker.

* `Source Path` Both in main.tf and README.md files, point the source to respective module terraform registry path.

    E.g:  

    source  = "terraform-ibm-modules/logdna/ibm//modules/instance"

* `Github actions` - GitHub Actions makes it easy to automate all the software workflows. As part of github actions we add pre-commit hooks which are being used to validate the PR before it gets merged onto main branch. It also being used to run the test cases perodically to assure the quality of both templates and the modules.

* `test directory` - Use terratest to write the test cases under `test` directory, which will be executed by the github actions using a scheduler on a periodic basis. Following link can be used as a reference to write a test file (https://github.com/terraform-ibm-modules/terraform-ibm-iam/blob/main/test/access-group/access_group_test.go)

* `.gitignore` -  Use this file to specify intentionally the untracked files that Git should ignore.

* `.pre-commit-config.yaml` - Used for identifying simple issues before submission to code review. We run our hooks on every commit to automatically point out issues in code such as missing semicolons, trailing whitespace, and debug statements. 
     