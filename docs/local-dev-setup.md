# Local development setup :id=dev-setup

?> _TODO_: update the content to work with modules in `terraform-ibm-modules` in GitHub.

Follow these steps to set up your local development environment for working with the `terraform-ibm-modules` project.

For regular maintenance tasks or to run certain pre-commit hooks manually, see [Regular developer tasks](dev-maintenance.md).

## Before you begin :id=dev-setup-prereqs

- On macOS and Linux systems, [install](https://docs.brew.sh/Installation) or [update](https://docs.brew.sh/FAQ) Homebrew.
- On Microsoft Windows, set up Windows Subsystem for Linux [WSL](https://ubuntu.com/wsl) and run commands within WSL.

## Clone and initialize the repo :id=dev-setup-clone

1.  Clone the repo you want to start working with:

    - To clone by using SSH, run the following command. You need a valid SSH key for github.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

        ```bash
        git clone git@github.com:terraform-ibm-modules/<REPO_NAME>.git
        ```

    - To clone by using HTTPS, run the following command.

        ```bash
        git clone https://github.ibm.com:terraform-ibm-modules/<REPO_NAME>.git
        ```

        Where `<REPO_NAME>` is an existing `terraform-ibm-modules` repo.

1.  Change directory to the root of the newly cloned repo and create a branch to work in:

    ```bash
    cd <REPO_NAME>
    git checkout -b ＜NEW-BRANCH＞
    ```

1.  Initialize the Git submodule:

    ```bash
    git submodule update --init
    ```

## Add the dependencies :id=dev-setup-add-deps

!> **Important** This approach installs the dependency binary files to your `/usr/local/bin` directory and overwrites the existing versions.

1.  Make sure that you have a current version of Python 3 and pip.
1.  Make sure that a recent stable version of [Go is installed](https://go.dev/doc/install) and available in your PATH environment variable.
1.  From the root directory of the repo, run the following command to set up all the necessary tools, including the pre-commit hooks:

    ```bash
    make
    ```

## Next steps :id=dev-setup-next-steps

That's it. Your development environment is set up the `terraform-ibm-modules` project. Now start coding.

- [Create a module](https://github.com/terraform-ibm-modules/terraform-ibm-module-template)

?> _TODO_: point instead to the tutorial for a single module. (need to make available)
