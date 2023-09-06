# Contributing to the IBM Cloud Terraform modules project

To create a module, you start from the module template. To update a module, you create a branch off the dev branch of the module you want to work with. Then, modify the Terraform logic, create examples, and run tests.

The process to create a module has several goals.

- To maintain the quality of IBM Cloud Terraform modules.
- To fix problems that are important to users.
- To engage the community in working toward the best Terraform modules for IBM Cloud.

Follow these steps to create or update a module.

## Before you begin

- If you're running Microsoft Windows, set up Windows Subsystem for Linux [WSL](https://ubuntu.com/wsl) and run commands within WSL.
- Make sure that you have a current version of Python 3 and pip. 
  - To check your installed version, run `python --version`.
- Make sure that you have a recent stable version of [Go](https://go.dev/doc/install) installed and available in your PATH environment variable.

## Request a repo

?> **Tip:** If you're updating an existing module, skip to the next step.

Submit a request for a new module repo in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose) with your idea for a module.

[inc-module-name-desc](inc-module-name-desc.md ':include')

When your repo is created, return to this topic and continue the steps.

## Clone and initialize the repo

Clone either the repo that you just created or the module repo that you want to update.

[inc-clone.md](inc-clone.md ':include')

## Add the dependencies

[inc-make](inc-make.md ':include')

## Update the repo name and description in source control

[inc-name-settings](inc-name-settings.md ':include')

## Update the Terraform files

1.  From the root of the newly cloned repo, create a branch to work in by running the command `git checkout -b ＜YOUR_TOPIC_BRANCH>`. Replace `＜YOUR_TOPIC_BRANCH>` with your own branch name.
1.  Implement (or update) the logic for your module by updating the `main.tf`, `version.tf`, `variables.tf`, and `outputs.tf` Terraform files.

    - For more information about module structure and guidance, see [Authoring guidelines](implementation-guidelines.md).
    - For more information about Terraform for IBM Cloud, see [Creating Terraform on IBM Cloud templates](https://cloud.ibm.com/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-create-tf-config) in the IBM Cloud docs.

## Create or update examples

Create or update at least one end-to-end example to test your code changes.

1.  Implement (or update) the logic for your module examples by updating the `main.tf`, `version.tf`, `variables.tf`, and `version.tf` Terraform files in the `examples/default` directory.
1.  Update the `README.md` file in the same examples directory to provide some basic information about what the example does.

[inc-examples](inc-examples.md ':include')

## Run examples and clean up

Run your examples to test the logic. After the examples run, destroy the resources.

1.  Set the environment variables that the test uses.

    1.  Set the `ibmcloud_api_key` variable as an environment variable.

        ```bash
        export TF_VAR_ibmcloud_api_key=<YOUR_API_KEY>
        ```

        Replace `<YOUR_API_KEY>` with the value of the API key that you want to use to test the code.

1.  In the `examples/default` directory, initialize the module to pull the dependencies.

    ```bash
    terraform init
    ```

1.  Apply the configuration and run the example.

    ```bash
    terraform apply
    ```

    Confirm that you want Terraform to apply the changes by typing `yes`. If everything runs successfully, you validated your Terraform logic.

1.  Clean up.

    1.  Run the following command to remove the resources that the example created.

        ```bash
        terraform destroy
        ```

    1.  Confirm that you want Terraform the destroy the resources by typing `yes`.

## Update the PR tests

Now that you tested the module by running your examples directly, update the `pr_test.go` file to run the examples as a unit test. This file runs as part of pull request pipelines. For more information about testing modules in this project, see [Tests](tests.md).

[tests.md](inc-tests-create.md ':include')

## Run the PR tests

[example-test](inc-example-test.md ':include')

For more information about testing modules in this project, see [Tests](tests.md).

## Commit your code and submit for review

After your PR tests pass, create a pull request.

When the PR is merged, your commit messages might change because the merging team uses the [squash and merge](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges#squash-and-merge-your-pull-request-commits) option to merge PRs. The PR commit message determines whether a new version of a module is needed and which [semantic versioning number](versioning.md) to use. The message also is published in the release notes for the module.

1.  Locally merge (or rebase) the upstream `main` branch into your topic branch:

    ```bash
    git pull [--rebase] upstream main
    ```
1.  Run the pre-commit hooks from the root of the repo to identify other changes that you need to make:

    ```bash
    pre-commit run --all-files
    ```

1.  Iteratively address all the issues from this check, commit the changes, and run the `pre-commit` command until all tests pass. For example, commit changes to the readme file that is updated from the pre-commit hooks.
1.  Push your topic branch to your repo:

    ```bash
    git push origin ＜YOUR_TOPIC_BRANCH>
    ```

1.  Open a pull request:

    1.  Start by contributing a draft PR. A draft pull request provides insight about the work that you're doing but cannot be merged. To create a draft pull request, use the drop-down and select **Create Draft Pull Request**, then click **Draft Pull Request**.
        - Open your PR from your branch to `main`.
        - Provide a clear title and description. Be sure to merge the latest changes from upstream before you create the PR.
    1.  When you're ready to merge your code, mark your draft pull request as ready for review. For more information, see [Changing the stage of a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request).
    1.  Run the CI pipeline workflow by adding a comment to the PR with the following text:

        ```text
        /run pipeline
        ```

        For more information about workflows, see [GitHub Actions workflows](gh-actions.md).

!> **Important** By contributing content, you agree to allow the project owner to license your work under the same license as that used by the project.

## Next steps

After the initial merge of a new repo, enable the upgrade test in `tests/pr_test.go`.

When you create a repo from the module template, the upgrade test is disabled by default. You can't run an upgrade test until the initial module code is merged to the main branch.

Create a pull request to enable the upgrade test in `pr_test.go` by commenting out the line that starts with `t.Skip`.
