# Validation tests

Tests are written in the Go programming language to take advantage of an open source Go library called [Terratest](https://github.com/gruntwork-io/terratest).

The tests also use test helper functions from [ibmcloud-terratest-wrapper](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper) ([source](https://github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper)).

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

    - If you must implement a breaking change to the module in a PR, include a Conventional Commit footer in one of the commits with the text `BREAKING CHANGE:` at the beginning of the footer. For more information, see the [Conventional Commits cheat sheet](https://cheatography.com/albelop/cheat-sheets/conventional-commits/).
    - If the change breaks example code but not module code, include `SKIP UPGRADE TEST` in the commit message. Make sure to describe why you are breaking the example in the PR description.

  ?> **Tip**: The upgrade test is disabled by default in `pr_test.go` in the module template because you can't run an upgrade test until the initial module code is merged to the main branch. After the initial merge, create a pull request to enable the upgrade test by commenting out the line that starts with `t.Skip`.

- **IBM Cloud Schematics test**

    Use the `testschematic/TestSchematicOptions.RunSchematicTest()` function to execute a test example from within an IBM Cloud Schematics Workspace.
    - Sets up a new transient workspace in your account to execute tests
    - Configurable tar file is built that is uploaded to workspace
    - `init`, `apply`, and `destroy` actions for workspace are executed
    - Workspace is deleted on successful test
    - Supports setting of Workspace environment variables
    - Supports Schematic Variablestore settings for test input variables
    - netrc settings can be configured to support terraform modules in private github source locations

[Examples](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testschematic#pkg-overview) can be found at offical repository.

### The other_test.go file

Use the [other_test.go](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/tests/other_test.go) file to test end-to-end examples that are not run in `pr_test.go`. The tests in this file don't run in the PR pipeline, but are run in the continuous testing pipeline (internally).

## Creating tests

[tests.md](inc-tests-create.md ':include')

## Running the tests

[example-test](inc-example-test.md ':include')

## Other test customizations

### Review all test options available

The test option objects `TestOptions` and `TestSchematicOptions` have many fields that can be used to further configure your test runs. You can review all of the current options available at the official Go package repository for `ibmcloud-terratest-wrapper`.
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

### More Examples

For more examples of various test customization, you can consult the official Go package repository for `ibmcloud-terratest-wrapper`.
- [Terratest Examples](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testhelper#pkg-overview)
- [Schematics Workspace Examples](https://pkg.go.dev/github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper/testschematic#pkg-overview)
- [README Examples](https://github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper#readme)