# Validation tests

Tests are written in the Go programming language to take advantage of an open source Go library called [Terratest](https://github.com/gruntwork-io/terratest).

The tests also use test helper functions from the [ibmcloud-terratest-wrapper](https://github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper) module. For more information about the functions, see the Go package at [pkg.go.dev](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper).

To test the module, you test the example code in the `examples` folder.

## Types of tests

### The pr_test.go file

In the [pr_test.go](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/tests/pr_test.go) file, include all tests that you want to run in the PR pipeline

Make sure that you include at least these two tests:

- **Terraform init, apply, and destroy test**

    Use the `RunTestConsistency()` test helper to run this test. This function runs the following commands:
    - Runs `terraform init` and `terraform apply`.
    - Runs `terraform plan` to ensure idempotency if the init and apply commands pass.

        The test fails if the plan identifies any changes (in other words, the module is not idempotent). Some modules have expected changes. For more information about how to address expected changes, see the following [Ignoring expected changes](#ignoring-expected-changes) section.
    - Runs `terraform destroy` at the end of the test, whether the previous commands pass or fail.

- **Upgrade test**

    Use the `RunTestUpgrade()` test helper to help determine compatibility with earlier module versions.

  ?> **Tip**: If you're working on the first PR for a module, skip the upgrade in `pr_test.go` because you can't run an upgrade test until the initial module code is merged to the main branch. To skip the test, include `SKIP UPGRADE TEST` in the commit message. Include information about why you're skipping the test. If you realise that you no longer want to skip the upgrade test in the PR, comment `UNSKIP UPGRADE TEST` in the commit message.

- **IBM Cloud Schematics test**

    Use the `testschematic/TestSchematicOptions.RunSchematicTest()` function to execute a test example from within an IBM Cloud Schematics Workspace. The function includes the following things:
    - Sets up a new transient workspace in your account to execute tests
    - Builds a configurable .tar file that is uploaded to the workspace
    - Executes `init`, `apply`, and `destroy` actions for the workspace
    - Deletes the workspace after a successful test
    - Supports setting workspace environment variables
    - Supports Schematics `variablestore` settings for test input variables
    - Allows `.netrc` settings to support Terraform modules in private GitHub source locations

    For more information, see the [examples](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testschematic#pkg-overview) at pkg.go.dev.

### The other_test.go file

Use the [other_test.go](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/tests/other_test.go) file to test end-to-end examples that are not run in `pr_test.go`. The tests in this file don't run in the PR pipeline, but are run in the continuous testing pipeline (internally).

## Creating tests

[tests.md](inc-tests-create.md ':include')

## Running the tests

[example-test](inc-example-test.md ':include')

## Other test customizations

### TestOptions and TestSchematicOptions

You can configure your tests by using the fields in the `TestOptions` and `TestSchematicOptions` objects:
- [TestOptions](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testhelper#TestOptions)
- [TestSchematicOptions](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testschematic#TestSchematicOptions)

### TestOptionsDefaultWithVars() vs TestOptionsDefault()

Many examples require the same four input variables, `region`, `prefix`, `resource_group`, and `resource_tags`.

- If your example uses all four of those variables, use `TestOptionsDefaultWithVars()`. The function is used in the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/examples/default/variables.tf).
- If your example doesn't require all four variables, use `TestOptionsDefault()` with `options.TerraformVars` to pass the variables that the example needs.

### Ignoring expected changes

By default, the `RunTestConsistency()` test helper fails if it identifies changes after the initial `terraform apply` completes successfully. Some modules make changes, such as `null_resource` blocks that use an `always_run` trigger. To handle expected changes, you can configure the test to ignore the expected changes and pass.

Both `TestOptionsDefaultWithVars()` and `TestOptionsDefault()` support passing values for `IgnoreDestroys`, `IgnoreUpdates`, and `IgnoreAdds`. (`IgnoreAdds` is ignored during an upgrade test because additions are a valid use case for an upgrade test).

### Speed up tests by using implicit destroy

Tests can take a long time to run, for example when they provision and then destroy resources that take time to complete. One way to speed up the tests is to use the `ImplicitDestroy` feature. This feature explicitly passes objects from the state file that can be removed before a `destroy` is run.

For example, if a test spins up a Kubernetes cluster and then deploys things to it, you can use `ImplicitDestroy` to remove all the resources that are deployed. The resources are destroyed along with the cluster deletion.

!> **Important** Never pass any resources to `ImplicitDestroy` that are created as part of the module that you are testing. The tests are designed to follow the same flow as a user who runs `terraform destroy`. Use this feature only on supporting resources of the module that are used in the end-to-end test.

### More examples

For more examples of test customization, see the pkg.go.dev repository and the GitHub repo for `ibmcloud-terratest-wrapper`:
- [Terratest examples](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testhelper#pkg-overview)
- [Schematics Workspace examples](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testschematic#pkg-overview)
- [Usage examples](https://github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper) in the GitHub repo.
