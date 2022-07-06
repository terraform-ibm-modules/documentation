# Reusable GitHub Actions workflows

You use GitHub Actions workflows to run CI/CD pipelines in your modules. The reusable workflows are sourced in the [Common pipeline assets](https://github.com/terraform-ibm-modules/common-pipeline-assets/tree/main/.github/workflows) repository.

The following reusable workflows are included in the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/) repo.

- `common-terraform-module-ci` for pull requests and merges into main branch.

    Called from `/.github/workflows/ci.yml`.
- `common-release` for semantic release version tagging. The workflow is run after the CI pipeline successful completes on the main branch.

    Called from `/.github/workflows/release.yml`.
