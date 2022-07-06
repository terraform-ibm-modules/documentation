# Contributing to the documentation

## Creating or updating content

If you want to make a small change, click **Edit in GitHub** at the top of any docs page. Clicking the link takes you to the .md file where you can make your changes and create a pull request for a review.

When changes are merged to the main branch, they are built and published to https://terraform-ibm-modules.github.io/documentation/. So, changes can't go into the branch until they are reviewed, edited, and approved by a one of the doc maintainers.

?> _Tip_: If you'd rather give feedback about the documentation, create an issue in the [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues). For more information, see [Report an issue or request a feature](support.md).

### Making content changes locally

Fork the repo so you can work locally. You can [preview your changes](/contributing-docs.md#previewing-the-docs-locally) before you create a pull request.

1.  Fork the documentation repo.
1.  Create a working branch from the `main` branch.
1.  Make your changes to the Markdown content.
1.  Commit your updates.
1.  Create a pull request from your branch to `main`.

    Link the PR to an issue if you're addressing one. For more information about how to link them, see the [GitHub docs](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue).

The documentation team reviews your PR and might request changes. If the changes are relatively straightforward and self-contained, such as a corrected typo or a rewritten sentence, we will approve and merge them into draft after issues are addressed.

If the changes are more extensive, such as a significant rewrite or entirely new content, the documentation team might need to make revisions for editorial or style reasons. In this case, we might open a new PR against your branch with our proposed revisions. You can then review these revisions and incorporate the changes into your branch. After the documentation team is satisfied with the proposed changes, we merge your PR.

### Previewing the docs locally

To work on documentation and be able to view the rendered content create a local environment. For more information, see the [docsify site](https://docsify.js.org/#/quickstart).


1.  Install docsify-cli

    ```bash
    npm i docsify-cli -g
    ```
1.  From the root directory of the project, run the following command to preview the docs from your local server:

    ```bash
    docsify serve docs -o
    ```

    The command opens the docs in your default browser at http://localhost:3000.

1.  To update content, create or update the Markdown files in the `docs` directory.

    The left navigation window is defined in the `_sidebar.md` file.
