# Local development setup :id=dev-setup

?> _TODO_: update the content to work with modules in `terraform-ibm-modules` in GitHub.

Follow these steps to set up your local development environment for Project GoldenEye.

## Before you begin :id=dev-setup-prereqs

- On macOS and Linux systems, [install](https://docs.brew.sh/Installation) or [update](https://docs.brew.sh/FAQ) Homebrew.
- On Microsoft Windows, set up Windows Subsystem for Linux [WSL](https://ubuntu.com/wsl) and run commands within WSL.

For regular maintenance tasks or to run certain pre-commit hooks manually, see [Regular developer tasks](/docs/solution-as-code?topic=solution-as-code-dev-maintenance).

## Set the protocol for remotes and submodules :id=dev-setup-protocol

By default, GoldenEye uses HTTPS to connect to remote repositories on GitHub Enterprise (github.ibm.com) and to pull in Terraform submodules. To avoid the prompt for credentials when you connect to a remote (for example, working with Git submodules or importing Terraform modules), choose one of the following options:

- Update your local Git config file to use SSH for access to github.ibm.com/GoldenEye.

    ```bash
    git config --global url."git@github.ibm.com:GoldenEye".insteadOf "https://github.ibm.com/GoldenEye"
    ```

    Or

- Create a `.netrc` file that includes your Git token to continue to use HTTPS.

    ```bash
    export GH_TOKEN=XXX
    echo -e "machine github.ibm.com\n  login $GH_TOKEN" >> ~/.netrc
    ```

    Where `XXX` is the value of your Git token.

## Clone and initialize the repo :id=dev-setup-clone

1.  Clone the repo you want to start working with:

    - To clone by using SSH, run the following command. You need a valid SSH key for github.ibm.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

        ```bash
        git clone git@github.ibm.com:GoldenEye/<REPO_NAME>.git
        ```

    - To clone by using HTTPS, run the following command.

        ```bash
        git clone https://github.ibm.com:GoldenEye/<REPO_NAME>.git
        ```

        Where `<REPO_NAME>` is an existing GoldenEye repo.

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

Choose the method to add the dependencies:

- [Use the Docker image](#option-1-docker) (recommended)
- [Install dependencies locally](#option-2-install)

### Option 1. Use the Docker image (recommended) :id=option-1-docker

You can use the `goldeneye-ci-image` to do local development and testing. The image includes all the required dependencies at the same version levels that are used by all the GoldenEye CI tests.

1.  Make sure that the Docker runtime is installed on your development environment
1.  Run the following command to pull the image locally. The image is available to IBMers by using Artifactory credentials.

    ```bash
    make docker-pull ARTIFACTORY_USERNAME=user@ibm.com ARTIFACTORY_PASSWORD=XXX
    ```

    Pull the latest stable image regularly so that you have the most recent version. The image is built every day.
1.  Run the following command from the root directory of the repo:

    ```bash
    make docker-run
    ```

    After you run the command, your command line runs inside the Docker container. The root repository, `~/.ssh`, `~/.netrc`, and `~/.gitconfig` are all mounted so that your local GitHub protocol settings are also set inside the Docker runtime. Use this session to run any Terraform or Terratest commands.

1.  Run the following command to install all pre-commit hooks:

    ```bash
    make dependency-pre-commit
    ```

### Option 2. Install dependencies locally :id=option-2-install

This approach installs the dependency binary files to your `/usr/local/bin` directory and overwrites the existing versions.

1.  Make sure that you have a current version of Python 3 and pip.
1.  Make sure that a recent stable version of [Go is installed](https://go.dev/doc/install) and available in your PATH environment variable.
1.  From the root directory of the repo, run the following command to set up all the necessary tools, including the pre-commit hooks:

    ```bash
    make
    ```

## Next steps :id=dev-setup-next-steps

That's it. Your development environment is set up for Project GoldenEye. Now start coding.

- [Create a module](/docs/solution-as-code?topic=solution-as-code-getting-started-contrib)
- [Update a module](https://github.ibm.com/GoldenEye/documentation/blob/master/modules-list.md)
