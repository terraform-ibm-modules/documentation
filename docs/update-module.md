# Updating a module

When you have improvements or fixes to a module or want to address limitations, you can contribute updates. You fork the module you want to work with.

?> **Tip:** If you're creating a module, see [Contributing to the IBM Cloud Terraform modules project](/contribute-module.md).

## Overall process

1.  Set up your development environment.
1.  Fork the repo and clone it locally.
1.  Make your changes.
1.  Test your changes with example code.
1.  Open a pull request.

## Before you begin

[inc-prereqs-dev.md](inc-prereqs-dev.md ':include')

## Fork, clone, and initialize the repo

Fork the module repo that you want to update.

1.  Navigate to the repository that you want to update.
1.  Fork the repo by clicking **Fork** in the top-right corner of the page.

    - Clear the **Copy the main branch only** option to copy all branches to your fork.
    - If you plan to create another module from this code, type a new repository name.
1.  Clone your fork:

    - To clone by using SSH, run the following command. You need a valid SSH key for github.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

        ```bash
        gh clone git@github.com:<REPO_OWNER>/<REPO_NAME>.git
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

    For more information, see [Configuring a remote repository for a fork](https://docs.github.com/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-repository-for-a-fork?platform=mac).

1.  Initialize the Git submodule:

    ```bash
    git submodule update --init
    ```

## Add the dependencies

[inc-make](inc-make.md ':include')

## Update the Terraform files

[inc-tf-update.md](inc-tf-update.md ':include')


## Update examples

If necessary, update the end-to-end examples to test your code changes.

1.  Update the logic for your module examples by updating the `main.tf`, `version.tf`, `variables.tf`, and `version.tf` Terraform files in the `examples/default` directory.
1.  Update the `README.md` file in the same examples directory to provide some basic information about what the example does.

### About end-to-end examples

[inc-examples](inc-examples.md ':include')

## Run examples and clean up

[inc-examples-run](inc-examples-run.md ':include')

## Commit your code and submit for review

### Verify changes

[inc-precommit](inc-precommit.md ':include')

### Open a pull request

Start by contributing a draft PR. A draft pull request provides insight about the work that you're doing but cannot be merged.

1.  To create a draft pull request in GitHub, use the drop-down and select **Create Draft Pull Request**, then click **Draft Pull Request**.
    - Open your PR from your branch to `main`.
    - Provide a clear title and description. Be sure to merge the latest changes from upstream before you create the PR.
1.  When you're ready to merge your code, mark your draft pull request as ready for review. For more information, see [Changing the stage of a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request).

When the PR is merged, your commit messages might change because the merging team uses the [squash and merge](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges#squash-and-merge-your-pull-request-commits) option to merge PRs. The PR commit message that's included by the merging team determines whether a new version of a module is needed and which [semantic versioning number](versioning.md) to use. The message also is published in the release notes for the module.
