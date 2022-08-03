# Update an older module

Module repos created before July 2022 don't include the logic that is needed to pass the continuous integration (CI) tests and to publish the modules to the IBM Cloud catalog. Follow these steps to update an existing repo in the terraform-ibm-modules GitHub organization.

## Before you begin

- If you're running Microsoft Windows, set up Windows Subsystem for Linux [WSL](https://ubuntu.com/wsl) and run commands within WSL.
- Make sure that you have a current version of Python 3 and pip.
- Make sure that you have a recent stable version of [Go](https://go.dev/doc/install) installed and available in your PATH environment variable.

## Create an empty module

Create an empty module repo in the `terraform-ibm-modules` GitHub organization.

1.  In the upper right of any page in the [terraform-ibm-modules](https://github.com/terraform-ibm-modules) organization, use the **+** menu, and select **New repository**.
1.  Select `terraform-ibm-modules` as the owner.
1.  Enter a name for the module in format `terraform-ibm-<NAME>`, where `<NAME>` reflects the type of infrastructure that the module manages. Use hyphens as delimiters for names with multiple words (for example, terraform-ibm-`activity-tracker`).
1.  Provide a short description of the module. The description is displayed under the repository title on the [organization page](https://github.com/terraform-ibm-modules) and in the **About** section of the repository. Use the description to help users understand what your repo does by looking at the description.
1.  Confirm that you are creating a public repository in the terraform-ibm-modules organization and click **Create repository**.

## Clone and initialize the repo

Clone the repo that you just created.

[inc-clone.md](inc-clone.md ':include')

## Migrate the module code

1.  From the root of the newly cloned repo, create a branch to work in by running the command `git checkout -b ＜YOUR_WORKING_BRANCH>`. Replace `＜YOUR_WORKING_BRANCH>` with your own branch name.
s
1.  Push the module code from the older repo to the new one by running these commands:
    1.  Add the new repo as a remote to the older repo:

        ```bash
        git remote add origin2 https://github.com/terraform-ibm-modules/<REPO_NAME>
        ```

        Where `<REPO_NAME>` is your new repo. The command uses `origin2` because Git uses `origin` by default.
    1.  Check that the remote points from your old repo to the new one by running this command:

        ```bash
        git remote -v
        ```
    1.  Push the module code from the older repo to the main branch of the new repo:
        ```bash
        git push origin2 main
        ```

## Add the newer CI/CD code

Copy the following files from the `.github` directory of the terraform-ibm-module-template.

1.  Browse to the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/.github) `.github` directory.
1.  Copy the `settings.yml` file.
1.  Copy the `workflows` directory that contains the GitHub Action workflow

## Make updates to pass the pre-commit checks

1.  Run the pre-commit hooks From the root of the newly cloned repo to identify other changes that you need to make:

    ```bash
    pre-commit run --all-files
    ```

1.  Iteratively address all the issues from this check, commit the changes, and run the `pre-commit` command until you have a clean check.

## Create or update examples

Create or update at least one end-to-end example to test your code changes. You can see the structure in the [examples](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/tree/main/examples) directory of the terraform-ibm-module-template.

1.  Implement (or update) the logic for your module examples by updating the `main.tf`, `version.tf`, `variables.tf`, and `version.tf` Terraform files in the `examples/default` directory.
1.  Update the `README.md` file in the same examples directory to provide some basic information about what the example does.

[inc-examples](inc-examples.md ':include')

## Run examples and update the PR tests

Validate your Terraform logic by running the examples. Then update the test scripts to run the examples with pull requests.

1.  Run your examples to test the logic. For more information, see [run examples and clean up](contribute-module.md#run-examples-and-clean-up) in the docs.

    After the examples run, destroy the resources.
1.  Copy the contents of the [tests](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/tree/main/tests) directory from the terraform-ibm-module-template.
1.  Update the `pr_test.go` file to run the examples as a unit test. For more information, see [Update the PR tests](contribute-module.md#update-the-pr-tests) in the docs.

## Open an initial pull request

Open a pull request from your working branch in the new repo to the `main` branch.

After the CI pipeline passes and the PR is merged, automation creates a GitHub semantic version release and publishes the module to the IBM Cloud catalog as a private entry initially. For more information about the CI pipeline, see [Tests](tests.md).

## Next steps

Archive the older repo in GitHub. Update the `readme` file to point to the new repo.
