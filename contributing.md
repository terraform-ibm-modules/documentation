# Welcome to IBM Cloud Terraform Modules contributing guide :id=contribute

!> **Important** Much of the organization of this content is taken from [GitHub Docs](https://github.com/github/docs/blob/main/CONTRIBUTING.md).

?> *TODO* Replace the `contribution_guidelines.md` file in [/terraform-ibm-modules/getting-started](https://github.com/terraform-ibm-modules/getting-started) with this kind of information

Thank you for taking the time to contribute to our project!

You can contribute to the modules or this documentation, or you can create modules The following types of contributions might give you ideas about what you can contribute.

- Limitations in a current module
- Improvements and fixes to existing modules
- New solutions that address your use cases

Although code is a common contribution, we're also looking for other contributions to help the effort, such as documentation updates, new ideas, and bug reports. Post an issue in the [issue tracker repo](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues) if you want to chat about it.

TODO: Perhaps set up the `Discussion` section in either the docs or issue tracker repos for discussing ideas, problems, etc.
{: important}

This project is built on your contributions. Delivering a draft is better than not contributing anything. Don't wait until you craft the perfect solution, start by providing your unpolished masterpiece. The maintainers can support you and help deliver something that works for the widest audience.

Read our [Code of Conduct](./CODE_OF_CONDUCT.md) to keep our community approachable and respectable.

TODO: Create code of conduct file for the repo
{: important}

In this guide you will get an overview of the contribution workflow from opening an issue, creating a PR, reviewing, and merging the PR.

<!-- Use the table of contents icon <img src="./assets/images/table-of-contents.png" width="25" height="25" /> on the top left corner of this document to get to a specific section of this guide quickly. -->

## New contributor guide
{: #contrib-new}

To get an overview of the project, read the [readme file](README.md). Here are some other resources to help you get started with contributions:

TODO: Flesh this out
{: important}

## Getting started
{: #contrib-gs}

TODO: Flesh this out
{: important}

- Tell me video?
- Authoring guidelines?
- Types of contributions

### Issues
{: #contrib-issues}

#### Create an issue
{: #contrib-issue-create}

If you spot a problem with a module or the docs, [search for an existing issue](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues). If a related issue doesn't exist, you can open a new issue by using a relevant [issue template](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose).

#### Solve an issue
{: #contrib-issue-solve}

Scan through our [existing issues](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues) to find one that interests you. As a rule, we don’t assign issues to anyone. If you find an issue to work on, you are welcome to open a PR with a fix.

### Make Changes
{: #contrib-changes}

TODO: Flesh this out
{: important}

1.  Submit issue with your idea for a module. (needs issue template in [terraform-ibm-issue-tracker](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/issues/new/choose){: external}).
1.  Meet the development prereqs.
1.  Create repo from template (need to update [terraform-ibm-module-template](https://github.com/terraform-ibm-modules/terraform-ibm-module-template){: external}).
1.  Add dependencies to new repo.
1.  Update Terraform logic.
1.  Create and run end-to-end example.
1.  Create and run tests against example.
1.  (Optional) Identify NIST controls
1.  Update readme file.
1.  (Optional) Onboard to IBM Cloud catalog.

### Commit your update
{: #contrib-commit}

When your changes are ready, don't forget to [self-review](/contributing/self-review.md) to speed up the review process.

### Pull Request
{: #contrib-prs}

When you're finished with the changes, create a pull request, also known as a PR.

- Complete the "Ready for review" template so that we can review your PR. This template helps reviewers understand your changes and the purpose of your pull request.
- Don't forget to [link PR to issue](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue) if you are solving one.
- Enable the checkbox to [allow maintainer edits](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/allowing-changes-to-a-pull-request-branch-created-from-a-fork) so the branch can be updated for a merge. After you submit your PR, a Docs team member will review your proposal. We might ask questions or request for additional information.
- We might ask for changes to be made before a PR can be merged, either by using [suggested changes](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/incorporating-feedback-in-your-pull-request) or pull request comments. You can apply suggested changes directly through the UI. You can make any other changes in your fork, and then commit them to your branch.
- As you update your PR and apply changes, mark each conversation as [resolved](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/commenting-on-a-pull-request#resolving-conversations).
- If you run into any merge issues, check out this [Git tutorial](https://github.com/skills/resolve-merge-conflicts) to help you resolve merge conflicts and other issues.

### Your PR is merged
{: #contrib-merged}

Congratulations! The team thanks you.
