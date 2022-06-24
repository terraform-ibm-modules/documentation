# Local development setup

Follow these steps to set up your local development environment for Project GoldenEye.

1.  Check the [prerequisites](#before-you-begin).
1.  [Clone and initialize the repo](#clone-and-initialize-the-repo).
1.  [Install the dependencies](#install-the-development-dependencies).

For regular maintenance tasks or to run certain pre-commit hooks manually, see [Regular developer tasks](dev-maintenance.md).

## Before you begin

- On macOS and Linux systems, [install](https://docs.brew.sh/Installation) or [update](https://docs.brew.sh/FAQ) Homebrew.
- On Microsoft Windows, set up Windows Subsystem for Linux [WSL](https://ubuntu.com/wsl) and run commands within WSL.

## Clone and initialize the repo

1.  Clone the repo you want to start working with:

    - To clone by using SSH, run the following command. You need a valid SSH key for github.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).
        ```sh
        git clone git@github.com:terraform-ibm-modules/<REPO_NAME>.git
        ```

    - To clone by using HTTPS, run the following command.
        ```sh
        git clone https://github.com:terraform-ibm-modules/<REPO_NAME>.git

        ```
        Where `<REPO_NAME>` is an existing `terraform-ibm-modules` repo.

1.  Change directory to the root of the newly cloned repo and create a branch to work in:
    ```sh
    cd <REPO_NAME>
    git checkout -b ＜NEW-BRANCH＞
    ```

1.  Initialize the Git submodule:

    ```sh
    git submodule update --init
    ```

## Add the dependencies

:exclamation: Important: This approach installs the dependency binary files to your `/usr/local/bin` directory and overwrites the existing versions.

1.  Make sure that you have a current version of Python 3 and pip.
1.  Make sure that a recent stable version of [Go is installed](https://go.dev/doc/install) and available in your PATH environment variable.
1.  From the root directory of the repo, run the following command to set up all the necessary tools, including the pre-commit hooks:

    ```sh
    make
    ```

## Next steps

That's it. Your development environment is set up for Project GoldenEye. Now start coding.

- [Create a module](https://github.com/terraform-ibm-modules/terraform-ibm-module-template)