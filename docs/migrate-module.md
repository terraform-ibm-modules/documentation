# Porting an older module

Modules in the IBM Terraform modules project need specific logic and workflows to pass the continuous integration (CI) tests and to publish the modules to the IBM Cloud catalog. To port a Terraform repo to these requirements and add it to the terraform-ibm-modules GitHub project, follow these steps.

For more information about how new modules are organized, see [module structure](module-structure.md).

?> Tip: If you want to contribute a new module instead of migrating one, follow the steps in [Contributing a module](contribute-module.md).

## Before you begin

- Make sure that you meet the prerequisites in the [Before you begin](local-dev-setup.md#before-you-begin) section of "Local development setup" in the docs.

## Request an empty module

Submit a request in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose) with your idea for a module.

[inc-module-name-desc](inc-module-name-desc.md ':include')

When your repo is created, return to this topic and continue the steps.

## Clone and initialize the repo

Clone the repo and configure the submodule.

1.  Navigate to the repository that you want to start working with.
1.  Fork the repo by clicking **Fork** in the top-right corner of the page.
1.  Clone your fork:

    - To clone by using SSH, run the following command. You need a valid SSH key for github.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

        ```bash
        git clone git@github.com:<REPO_OWNER>/<REPO_NAME>.git
        ```

    - To clone by using HTTPS, run the following command.

        ```bash
        git clone https://github.ibm.com/<REPO_OWNER>/<REPO_NAME>.git
        ```

    Where `<REPO_OWNER>` is the owner of the forked repository and `<REPO_NAME>` is the name of the repo you forked.
1.  Confirm the remote repository for your fork.

    1.  Locally, list the remote repo:

        ```bash
        git remote -v
        ```

    1.  If necessary, add or update the upstream repo. For example, if you use SSH, run this command:

        ```bash
        git remote add upstream git@github.com:terraform-ibm-modules/<REPO_NAME>.git
        ```

    For more information, see [Configuring a remote repository for a fork](https://docs.github.com/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-repository-for-a-fork).
1.  Add the Git submodule.

    ?> **Tip:** You can use the [migration script](https://github.com/terraform-ibm-modules/common-dev-assets/blob/main/repo_migration.sh) in the `common-dev-assets` repo to add the submodule and links.

    ```bash
    git submodule add https://github.com/terraform-ibm-modules/common-dev-assets
    ```

1.  Create symbolic links to the submodule by running these commands from the root of the module:

    ```bash
    ln -s common-dev-assets/module-assets/basic-pre-commit/.pre-commit-config.yaml .pre-commit-config.yaml
    git add .pre-commit-config.yaml
    ln -s common-dev-assets/module-assets/ci ci
    git add ci
    ln -s common-dev-assets/module-assets/Makefile Makefile
    git add Makefile
    ```

## Update the repo name and description in source control

[inc-name-settings](inc-name-settings.md ':include')

## Migrate your module code

Bring your Terraform logic from your older repo to the new repo.

1.  From the root of the newly cloned repo, create a branch to work in by running the command `git checkout -b ＜YOUR_WORKING_BRANCH>`. Replace `＜YOUR_WORKING_BRANCH>` with your own branch name.

1.  Push the module code from the older repo to the new one by running these commands. (You can copy the code if you don't want to use Git.)

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

## Add the newer CI code

Copy the following files from the `.github` directory of the terraform-ibm-module-template.

?> **Tip:** You can use the [migration script](https://github.com/terraform-ibm-modules/common-dev-assets/blob/main/repo_migration.sh) in the `common-dev-assets` repo to add the CI code.

1.  Browse to the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/blob/main/.github) `.github` directory.
1.  Copy the `settings.yml` file.
1.  Copy the `workflows` directory that contains the GitHub Action workflow

## Create or update examples

Create or update at least one end-to-end example to test your code changes. You can see the structure in the [examples](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/tree/main/examples) directory of the terraform-ibm-module-template.

?> **Tip:** You can use the [migration script](https://github.com/terraform-ibm-modules/common-dev-assets/blob/main/repo_migration.sh) in the `common-dev-assets` repo to add the CI code.

1.  Implement (or update) the logic for your module examples by updating the `main.tf`, `outputs.tf`, `provider.tf`, `variables.tf`, and `version.tf` Terraform files in the `examples/default` directory.
1.  Update the `README.md` file in the same examples directory to provide some basic information about what the example does.

[inc-examples](inc-examples.md ':include')

## Run examples and update the PR tests

Validate your Terraform logic by running the examples. Then, update the test scripts to run the examples with pull requests.

1.  Run your examples to test the logic. For more information, see [run examples and clean up](contribute-module.md#run-examples-and-clean-up) in the docs.

    After the examples run, destroy the resources.
1.  Copy the contents of the [tests](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/tree/main/tests) directory from the terraform-ibm-module-template.
1.  Update the `pr_test.go` file to run the examples as a unit test. For more information, see [Update the PR tests](contribute-module.md#update-the-pr-tests) in the docs.

## Make updates to pass the pre-commit checks

1.  Run the pre-commit hooks from the root of the newly cloned repo to identify other changes that you need to make:

    ```bash
    pre-commit run --all-files
    ```

1.  Iteratively address all the issues from this check, commit the changes, and run the `pre-commit` command until all tests pass. For example, commit changes to the readme file that is updated from the pre-commit hooks.

## Open an initial pull request

Open a pull request from your working branch in the new repo to the `main` branch.

After the CI pipeline passes and the PR is merged, automation creates a GitHub semantic version release and publishes the module to the IBM Cloud catalog as a private entry initially. For more information about the CI pipeline, see [Tests](tests.md).

## Next steps

Archive the older repo in GitHub. Update the `readme` file to point to the new repo.
