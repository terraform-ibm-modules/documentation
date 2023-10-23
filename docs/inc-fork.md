1.  Navigate to the repository that you want to update.
1.  Fork the repo by clicking **Fork** in the top-right corner of the page.

    If you plan to create another module from this code, type a new repository name.
1.  Clone your fork:

    - To clone by using SSH, run the following command. You need a valid SSH key for github.com. For more information, see the steps in the [GitHub docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

        ```bash
        git clone git@github.com:<REPO_OWNER>/<REPO_NAME>.git
        ```

    - To clone by using HTTPS, run the following command.

        ```bash
        git clone https://github.ibm.com/<REPO_OWNER>/<REPO_NAME>.git
        ```

    Where `<REPO_OWNER>` is the owner of the forked repository and `<REPO_NAME>` is the name of the repo you forked.
1.  Confirm the remote repository for your fork.

    1.  Locally, list the remote repo:

        ```bash
        git remote -v
        ```

    1.  If necessary, add or update the upstream repo. For example, if you use SSH, run this command:

        ```bash
        git remote add upstream git@github.com:terraform-ibm-modules/<REPO_NAME>.git
        ```

    For more information, see [Configuring a remote repository for a fork](https://docs.github.com/pull-requests/collaborating-with-pull-requests/working-with-forks/configuring-a-remote-repository-for-a-fork).
1.  Initialize the Git submodule:

    ```bash
    git submodule update --init
    ```
