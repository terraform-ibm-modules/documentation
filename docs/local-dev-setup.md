# Local development setup

Follow these steps to set up your local development environment for working with the `terraform-ibm-modules` project.

?> **Tip**: For regular maintenance tasks, see [Regular developer tasks](dev-maintenance.md).

## Before you begin

- Make sure that you have a current version of Python 3 and pip
  - To check your installed python version, run `python3 --version`.
  - To check whether "pip" is installed, run `python3 -m pip --version`.
- Make sure that a recent stable version of [Go is installed](https://go.dev/doc/install) and available in your PATH environment variable.
- On Microsoft Windows, set up Windows Subsystem for Linux [WSL](https://ubuntu.com/wsl) and run commands within WSL.

## Clone and initialize the repo

[inc-clone](inc-clone.md ':include')

## Add the dependencies

[inc-make](inc-make.md ':include')

## Next steps

That's it. Your development environment is set up the `terraform-ibm-modules` project. Now [contribute to a module](contribute-module.md).
