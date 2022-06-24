# Validation tests

Tests are written in the Go programming language to take advantage of an open source Go library called [Terratest](https://github.com/gruntwork-io/terratest).
The tests also use test helper functions from [ibmcloud-terratest-wrapper](https://github.com/terraform-ibm-modules/ibmcloud-terratest-wrapper).

To test the module, you test the example code in the `examples` folder.

## Types of tests

### [pr_test.go](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/tests/pr_test.go)

- Include all tests that you want to run in the PR pipeline in this PR test.
- Make sure that you include at least these two tests:
    - **Terraform init, apply, and destroy test**

      Use the `RunTestConsistency()` test helper to run this test. This function runs the following commands:
        - Runs `terraform init` and `terraform apply`.
        - Runs `terraform plan` to ensure idempotency if the init and apply commands pass.

          The test fails if the plan identifies any changes (the module is not idempotent) and some modules have expected changes. For more information about how to address changes, see the following [Ignoring expected changes](#ignoring-expected-changes) section.
        - Runs `terraform destroy` at the end of the test, whether the previous commands pass or fail.

    - **Upgrade test**

      Use the `RunTestUpgrade()` test helper to help determine compatibility with earlier module versions. If you must implement a breaking change to the module in a PR, include a Conventional Commit footer in one of the commits with the text `BREAKING CHANGE:` at the beginning of the footer. For more information, see the [Conventional Commits cheat sheet](https://cheatography.com/albelop/cheat-sheets/conventional-commits/).

      If the change breaks example code but not module code, include `SKIP UPGRADE TEST` in the commit message. Make sure to describe why you are breaking the example in the PR description.

      :information_source: The upgrade test is disabled by default in the [terraform-ibm-module-template pr_test.go](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/tests/pr_test.go) because you can't run an upgrade test until the initial module code is merged to the main branch. After the initial merge, create a pull request to enable the upgrade test by commenting out the line that starts with `t.Skip`.

### [other_test.go](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/tests/other_test.go)

- The tests in this file do not run in the PR pipeline. However, they are run in the continuous testing pipeline (internally).
- Use the `other_test.go` file to test end-to-end examples that are not run in `pr_test.go`.

## Creating tests

When you create tests for a new module, follow these steps.

1.  Use the latest templates from the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/tree/main/tests) and update the relevant code.

    - Configure the tests to use a separate resource group for each the module if you provision resources.
    - If you provision resources that require a resource group, work with the maintainers to create a resource group in the dev account for the new module.
1.  Update the module name in the `go.mod` file.
1.  Generate or update the `go.sum` file by running the following `make` command:

    ```sh
    make go-mod-tidy
    ```

    :information_source: This `make` command also supports a variable that is called `GO_MOD_ARGS` to pass more arguments to the `go mod tidy` command. For example, you can pass `GO_MOD_ARGS=-compat=1.18` to enforce compatibility with version 1.18.
1.  Ensure to commit any changes to the `go.mod` and `go.sum` files.

## Running the tests

1.  Set the following environment variables:
    - `IC_API_KEY` or `TF_VAR_ibmcloud_api_key`: An IBM Cloud API key for the account that the test uses to provision resources.
    - (Optional) `DO_NOT_DESTROY_ON_FAILURE`: Set this variable to `true` if you do not want to destroy resources when the test fails.
    - (Optional) `FORCE_TEST_REGION`: By default the tests select a region to provision resources in based on current region availability. This variable can be used to force a specific region, if required.
1.  Run the tests:

    - To run all tests:
        ```sh
        make run-tests-local
        ```
    - To run a specific test or tests, use the `RUN` variable to pass a regular expression that matches the names of the tests that you want to run:

        ```sh
        make run-tests-local RUN=TestRunDefaultExample
        ```

## Other test customizations

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

:exclamation: Never pass any resources to `ImplicitDestroy` that are created as part of the module that you are testing. The tests are designed to follow the same flow as a user who runs `terraform destroy`. Use this feature only on supporting resources of the module that are used in the end-to-end test.
