# Code owners

Every repository in the [terraform-ibm-modules](https://github.com/terraform-ibm-modules/) GitHub organization must have a primary and secondary code owner. 

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

## Code owner responsibilities

The primary code owner is responsible to comply with below list of code owner responsibilities. They should work closely with the secondary code owner and when needed delegate actions to them. The objective is to have a minimum of 2 experts who fully understand the code in the repository at all times.

### Pull request reviews

Code owners are automatically requested for review when someone opens a pull request that modifies code that they own, however it is not mandated that one of the code owners has to approve the pull request for it to be merged. If another core team member has the relevant skills to review the pull request, they can review and approve the pull request (NOTE: Every pull request must be approved by a core team member before it can be merged). It is however the code owners responsibility to ensure they remain up to date with the latest changes that go into a repository.

#### Renovate pull requests

Pull requests to keep dependency versions up to date are created by [renovate](renovate.md). It is the code owners responsibility to ensure that if a renovate created pull request fails the pipeline, that some action is taken. Actions could include:
- Re-running the pipeline if it failed on some transient issues
- Cloning the code to their own branch and creating a new pull request if a code change is required

!> **Important**: You should never manually close a renovate created pull request. If the pull request is no longer valid, or has conflicts etc, renovate will automatically close / update the pull request. If you manually close it and do not delete the renovate branch, new renovate pull requests will not be created!

?> **Tip**: It is also not recommended to commit directly to a renovate branch. If you do this, renovate will no longer manage the pull request. If this is done by accident, you can check the box in the pull request description that says "If you want to rebase/retry this PR, check this box" and on the next renovate run, it will override any changes you committed and force push a new renovate commit.

### Take action on incoming GitHub issues

It is the code owners responsibility to ensure they are aware of new GitHub issues that may get created in repository, and ensure they are handled appropriately. Actions could include:
- Identifying an appropriate owner and assigning (for core team owned repositories the issue will be synced internally so ensure the internal issue is assigned, or appropriate labels are added to the issue for someone to pick up from the prioritized backlog).
- Responding to the creator of the issue to let them know you have seen the issue, and provide any ETA or updates as needed.

### Respond to slack queries
Actively monitoring consumers slack queries in the `#terraform-ibm-modules` internal slack channel and if they are related to a repository in which you are a code owner for ensure to respond.

### Building up skills and keep up to date / current on latest in area
Be or become a Subject Matter Expert (SME) by building up skills and keeping up to date on latest in the relevant area. This would include working closely with the relevant IBM Cloud teams, attending blueprint talks / playbacks etc in order to be able to participate and drive in defining general functional directions in the area.
