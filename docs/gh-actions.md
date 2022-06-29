# Reusable GitHub Actions workflows

You use GitHub Actions workflows to run CI/CD pipelines in your modules. The reusable workflows are sourced in the [Common pipeline assets](https://github.com/terraform-ibm-modules/common-pipeline-assets/tree/main/.github/workflows) repository.

The following reusable workflows are included in the [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template/) repo.

- `common-terraform-module-ci` for pull requests and merges into main branch.

    Called from `/.github/workflows/ci.yml`.
- `common-release` for semantic release version tagging. The workflow is run after the CI pipeline successful completes on the main branch.

    Called from `/.github/workflows/release.yml`.

## How to call reusable workflows

If you need to call more reusable workflow files, use the following keywords and syntax:

- Call reusable workflow by using the `uses` keyword.
    - Refer to the workflow with `{owner}/{repo}/.github/workflows/{filename}@{ref}`. `{ref}` is a release version, not a branch name, for security reasons. The `renovate` task updates the reference to the most recent semantic version of reusable workflows.
- Use the `secrets: inherit` keyword to pass secrets from the module workflow. The common pipeline workflows use secrets in the [terraform-ibm-modules](https://github.com/terraform-ibm-modules) project.

For example, here's how the `common-terraform-module-ci` workflow is called in the module template.

```yaml
jobs:
  call-terraform-ci-pipeline:
    uses: terraform-ibm-modules/common-pipeline-assets/.github/workflows/common-terraform-module-ci.yml@v1.0.0
    secrets: inherit
```
