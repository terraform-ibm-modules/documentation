# Contributing to the IBM Cloud Terraform modules project

Create or update a Terraform module. When you create a module, you start from the template module. When you update a module, you fork the module. Then, modify the Terraform logic.

The process to create a module has several goals.

- To maintain IBM Cloud Terraform modules quality.
- To fix problems that are important to users.
- To engage the community in working toward the best possible Terraform modules for IBM Cloud.

## Overall process to contribute

?> _TODO_ Update these tasks to make sure they're in sync with the full process (including validation). Also, create tasks and conceptual information for this process

Follow these steps to contribute a new module. For more information, see the [guidelines for contributing](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/blob/main/README.md).

1.  Submit an issue in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose) with your idea for a module.

    ?> *TODO* (needs issue template in [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose)

1.  Meet the [development prerequisites](/docs/local-dev-setup.md).

1.  Start from an existing repo or the template:
    ?> *TODO* Update these steps to cover everything for new and updated repos.
    1.  If you're creating a module, follow these steps:
        1.  Create repo from the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template).
    1.  If you're updating a module, follow these steps:
        1.  Fork the project, clone your fork, and configure the remotes.

1.  Clone and initialize the repo. See [Local development setup](/local-dev-setup.md#dev-setup-clone).
1.  Commit your changes in logical chunks. Use Git's [interactive rebase](https://help.github.com/articles/interactive-rebase)
   feature to tidy up your commits before you make them public.
1.  Locally merge (or rebase) the upstream development branch into your topic branch:

    ```bash
    git pull [--rebase] upstream <dev-branch>
    ```
1.  Push your topic branch up to your fork:

    ```bash
    git push origin <topic-branch-name>
    ```
1.  Open a pull request with a clear title and description. Be sure to merge the latest from "upstream" before you create the PR.
1.  Make sure that the GitHub workflows are successfully running over the PR.

!> **Important** By contributing content, you agree to allow the project owner to license your work under the same license as that used by the project.
