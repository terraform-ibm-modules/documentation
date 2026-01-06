# Code owners

Every repository in the [terraform-ibm-modules](https://github.com/terraform-ibm-modules/) GitHub organization must have a primary and secondary code owner. Code owner responsibilities include maintaining the code base, participating in pull request reviews, and taking action on incoming GitHub issues.

## How to add / update repository code owners?

Code owners for a repository are stored in a file named `.github/CODEOWNERS`. The primary code owner should be listed first, followed by the secondary code owner. Below you will see the required format of the file where `primary-owner` and `secondary-owner` are the GitHub user names of the code owner users:

```
# Primary owner should be listed first in list of global owners, followed by any secondary owners
*       @primary-owner @secondary-owner
```

It is also possible to break down the owners per directory. For example:

```
# Primary owner should be listed first in list of global owners, followed by any secondary owners
*       @primary-owner @secondary-owner

# Order is important; the last matching pattern takes the most precedence. When someone opens a
# pull request that only modifies files in the below specified folders, only the listed owners
# and not the global owners will be requested for a review.
dev/ @dev-sre-user
stage/ @stage-sre-user
prod/ @prod-sre-user
```

For more information on the GitHub concept around code owners, see [About code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners).
