# Contributing to the IBM Cloud Terraform modules project for maintainers

Maintainers of the IBM Cloud Terraform modules project are responsible for creating and maintaining modules, and merging pull requests. Maintainers follow a set of guidelines to ensure that the module code is high quality and is maintained in a timely manner.

To create a module, request a repo and then fork the repo. To update a module, fork the repo that you want to work with. Then, modify the Terraform logic then create examples, and run tests.

?> **Tip:** If you're not a maintainer in the project, follow the instructions in [Contributing modules](contribute-module.md).

## Before you begin

[inc-prereqs-dev.md](inc-prereqs-dev.md ':include')


## Request a repo

?> **Tip:** If you're updating an existing module, skip to the next step.

Submit a request for a new module repo in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose) with your idea for a module.

[inc-module-name-desc](inc-module-name-desc.md ':include')

When your repo is created, return to this topic and continue the steps.

## Fork, clone, and initialize the repo

Fork either the repo that was just created or the module repo that you want to update.

[inc-fork.md](inc-fork.md ':include')

## Add the dependencies

[inc-make](inc-make.md ':include')

## Update the repo name and description in source control

[inc-name-settings](inc-name-settings.md ':include')

## Update the Terraform files

[inc-tf-update.md](inc-tf-update.md ':include')

## Create or update examples

Create or update at least one end-to-end example to test your code changes.

1.  Implement (or update) the logic for your module examples by updating the `main.tf`, `version.tf`, `variables.tf`, and `version.tf` Terraform files in the `examples` subdirectories.
1.  Update the `README.md` file in the same `examples` directories to provide some basic information about what each example does.

### About end-to-end examples

[inc-examples](inc-examples.md ':include')

## Run examples and clean up

[inc-examples-run](inc-examples-run.md ':include')

## Update the PR tests

Now that you tested the module by running your examples directly, update the `pr_test.go` file to run the examples as a unit test. This file runs as part of pull request pipelines. For more information about testing modules in this project, see [Tests](tests.md).

[tests.md](inc-tests-create.md ':include')

## Run the PR tests

[example-test](inc-example-test.md ':include')

For more information about testing modules in this project, see [Tests](tests.md).

## Push your code and submit for review

After your PR tests pass, create a pull request.

### Verify changes

[inc-precommit](inc-precommit.md ':include')

### Open a pull request

1.  Start by contributing a draft PR. A draft pull request provides insight about the work that you're doing but cannot be merged. To create a draft pull request, use the drop-down and select **Create Draft Pull Request**, then click **Draft Pull Request**.
    - Open your PR from your working branch to `main`.
    - Provide a clear title and description. Be sure to merge the latest changes from upstream before you create the PR.
1.  When you're ready to merge your code, mark your draft pull request as ready for review. For more information, see [Changing the stage of a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request).
1.  Run the CI pipeline workflow by adding a comment to the pull request with the following text:

    ```text
    /run pipeline
    ```

    For more information about workflows, see [GitHub Actions workflows](gh-actions.md).

When the PR is merged, your commit messages might change because the merging team uses the [squash and merge](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/about-pull-request-merges#squash-and-merge-your-pull-request-commits) option to merge PRs. The PR commit message that's included by the merging team determines whether a new version of a module is needed and which [semantic versioning number](versioning.md) to use. The message is also published in the release notes for the module.

!> **Important** By contributing content, you agree to allow the project owner to license your work under the same license as that used by the project.


## Next steps

After the initial merge of a new repo, enable the upgrade test in `tests/pr_test.go`.

When a module is created for you from the module template, the upgrade test is disabled by default. That's because you can't run an upgrade test until the initial module code is merged to the main branch.

1.  Create a pull request to enable the upgrade test in `pr_test.go` by commenting out the line that starts with `t.Skip`.
