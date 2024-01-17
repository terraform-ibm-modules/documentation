# Contributing to the IBM Cloud Terraform modules project

To create a module, you request a repo, and then fork the repo. To update a module, you fork the repo that you want to work with. Then, you modify the Terraform logic, create examples, and run tests.

?> **Tip:** Maintainers, follow the process in [Maintainers contribution process](maintain-module.md).

The process to create a module has several goals.

- To maintain the quality of IBM Cloud Terraform modules.
- To fix problems and add features that are important to users.
- To engage the community in working toward the best Terraform modules for IBM Cloud.

## Overall process

Follow these steps to contribute or update a module.

1.  New repo: [Request a repo](#request-a-repo).
1.  [Fork and clone the repo](#fork-clone-and-initialize-the-repo).
1.  [Make your code changes](#update-the-terraform-files).
1.  [Create or update examples](#create-or-update-examples) to demonstrate the common usage of the module.
1.  [Open a pull request](#push-your-code-and-submit-for-review).

## Request a repo

?> **Tip:** If you're updating an existing module, skip to the next step.

Submit a request for a new module repo in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose) with your idea for a module.

[inc-module-name-desc](inc-module-name-desc.md ':include')

When your repo is created, return to this topic and continue the steps.

## Fork, clone, and initialize the repo

Fork either the repo that was just created or the module repo that you want to update.

[inc-fork.md](inc-fork.md ':include')

## Update the Terraform files

[inc-tf-update.md](inc-tf-update.md ':include')

## Create or update examples

Create or update at least one end-to-end example to test your code changes.

1.  Implement (or update) the logic for your module examples by updating the `main.tf`, `version.tf`, `variables.tf`, and `version.tf` Terraform files in the `examples` subdirectories.
1.  Update the `README.md` file in the same `examples` directories to provide some basic information about what each example does.

### About end-to-end examples

[inc-examples](inc-examples.md ':include')

## Push your code and submit for review

After your PR tests pass, create a pull request.

### Open a pull request

1.  Start by contributing a draft PR. A draft pull request provides insight about the work that you're doing but cannot be merged. To create a draft pull request, use the drop-down and select **Create Draft Pull Request**, then click **Draft Pull Request**.
    - Open your PR from your working branch to `main`.
    - Provide a clear title and description. Be sure to merge the latest changes from upstream before you create the PR.

### Request a code review

When you're ready to merge your code, request a review. Your PR is reviewed by the module maintainers and the community.

1.  Add a `Ready for review` comment to the PR. The comment triggers automation that adds the `ready-for-review` label to your PR.
1.  Mark your draft pull request as ready for review. For more information, see [Changing the stage of a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/changing-the-stage-of-a-pull-request).

When the maintainers start a review, they add the `acknowledged` label to the PR. The maintainers review the code and provide feedback. They work with you to get the code ready to merge by setting up tests and ensuring that the pipeline passes. After the pipeline passes and the code is approved by the maintainers, the PR is merged into the main branch.

!> **Important** By contributing content, you agree to allow the project owner to license your work under the same license as that used by the project.
