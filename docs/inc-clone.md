1.  Clone the repo you want to start working with. Don't fork the repo. The common pipeline automation uses access tokens that are available only on PRs that are opened from branches off the repos.

    - To clone by using SSH, run the following command. You need a valid SSH key for github.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

        ```bash
        git clone git@github.com:terraform-ibm-modules/<REPO_NAME>.git
        ```

    - To clone by using HTTPS, run the following command.

        ```bash
        git clone https://github.ibm.com/terraform-ibm-modules/<REPO_NAME>.git
        ```

        Where `<REPO_NAME>` is an existing `terraform-ibm-modules` repo.

1.  Initialize the Git submodule:

    ```bash
    git submodule update --init
    ```
