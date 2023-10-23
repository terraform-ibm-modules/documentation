1.  Locally merge (or rebase) the upstream `main` branch into your topic branch:

    ```bash
    git pull [--rebase] upstream main
    ```
1.  Run the pre-commit hooks from the root of the repo to identify other changes that you need to make:

    ```bash
    pre-commit run --all-files
    ```

1.  Iteratively address all the issues from this check, commit the changes, and run the `pre-commit` command until all tests pass. For example, commit changes to the readme file that is updated from the pre-commit hooks.
1.  Push your topic branch to your repo:

    ```bash
    git push origin ＜YOUR_TOPIC_BRANCH>
    ```
