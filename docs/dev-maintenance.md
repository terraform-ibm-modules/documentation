# Regular developer tasks dev-maintenance

?> *TODO* update the content to work with modules in `terraform-ibm-modules` in GitHub.

Run these commands as needed after you set up your development environment. To set up your environment, see [Local development setup](local-dev-setup.md).

## Maintenance tasks :id=dev-maint-tasks

Run these commands to keep your environment up to date.

### Update the Docker image :id=dev-maint-update-docker

Regularly run the following command to pull the latest stable Docker image if you set up your environment [by using Docker](local-dev-setup.md#option-1-use-the-docker-image-recommended). The image is built every day.

```bash
make docker-pull ARTIFACTORY_USERNAME=user@ibm.com ARTIFACTORY_PASSWORD=XXX
```

### Update your local Git submodule version :id=dev-maint-update-local-sub

Renovate updates the Git submodule with automated pull requests, so the repos usually have the latest submodule. To make sure that you're using this version locally, run the following command in the repo that you're working with:

```bash
git submodule update
```

### Update the Git submodule version in source control to the latest :id=dev-maint-update-git-sub

You might want to update a repo’s Git submodule version to the latest before the Renovate automation has done so. To do this, run the following command and commit the changes as part of a pull request:

```bash
git submodule update --remote --merge
```

## Run the pre-commit hooks manually :id=dev-maint-run-pre-commit

The GoldenEye pre-commit hooks run against changed files when you commit changes to Git. To run the pre-commit hooks against all files, run the following command:

```bash
pre-commit run --all-files
```

## Set and audit a detect-secrets baseline :id=dev-maint-ds

The [detect-secrets](https://github.com/ibm/detect-secrets){: external} tool runs as a pre-commit hook to ensure that no secret values are committed to GitHub. You can run the following commands to update your local file and push changes.

### Set a baseline :id=dev-maint-ds-baseline

To rescan the repo for secrets and update the baseline, run the following command from the root directory. The command uses your local version of `detect-secrets` instead of the version that is defined in the pre-commit hook.

```bash
detect-secrets scan --update .secrets.baseline
```

The results are logged to the `.secrets.baseline` file. Commit the changes to the `.secrets.baseline` file.

### Audit a baseline :id=dev-maint-ds-audit

To audit the baseline and mark secrets as true or false positives, run the following command:

```bash
detect-secrets audit .secrets.baseline
```

Commit the `.secrets.baseline` file after the audit.
