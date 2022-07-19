When you create tests for a new module, follow these steps.

1.  Use the latest templates from the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/tree/main/tests) and update the relevant code.

    - Configure the tests to use a separate resource group for each the module if you provision resources.
    - If you provision resources that require a resource group, create an issue in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose) for the maintainers to create a resource group.

1.  Update the module name in the `tests/go.mod` file.
1.  Generate or update the `go.sum` file by running the following `make` command from the root of the repo:

    ```bash
    make go-mod-tidy
    ```

    This command downloads the Go packages.

  ?> **Tip**: The `make` command also supports a variable `GO_MOD_ARGS` to pass more arguments to the `go mod tidy` command. For example, you can pass `GO_MOD_ARGS=-compat=1.18` to enforce compatibility with version 1.18.

1.  Save changes to the `go.mod` and `go.sum` files.
