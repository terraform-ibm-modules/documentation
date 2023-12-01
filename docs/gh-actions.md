# Reusable GitHub Actions workflows

You use GitHub Actions workflows to run CI/CD pipelines in your modules. The reusable workflows are sourced in the [Common pipeline assets](https://github.com/terraform-ibm-modules/common-pipeline-assets/tree/main/.github/workflows) repository.

The following reusable workflows are included in the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/) repo.

- `common-terraform-module-ci` for pull requests and merges into main branch.

    - Called from `/.github/workflows/ci.yml`.
    - If you are in the `github-collaborators` team, you can run this workflow by adding a comment to the pull request with the following text:

        ```text
        /run pipeline
        ```

- `common-release` for semantic release version tagging. The workflow is run after the CI pipeline successful completes on the main branch.

    Called from `/.github/workflows/release.yml`.

*NOTE:* Pipelines do not run on private repos as the org secrets are not available when using the free GitHub actions plan. See free account limitations here https://github.com/pricing#compare-features
