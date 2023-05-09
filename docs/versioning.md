# Release versioning

Modules are updated regularly. The changes adhere to [semantic versioning](https://semver.org/), with releases labeled as `{major}.{minor}.{patch}`. [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) are used to identify module versions.

Release labels apply to both modules and submodules. For example, a major version change to a submodule results in a major release for the whole module. However, changes to examples do not drive release levels.

## Major version changes

A major version release affects the infrastructure that is deployed by the module.

The following examples identify a major release:

- Adding changes that can make updates to resources that are created in the previous version and that might impact day-to-day operations
- Adding changes that can destroy infrastructure that is created in the previous version

    The GitHub release notes document either how to avoid destroying infrastructure (for example, by migrating Terraform state) or describe a path that supports business continuity.

## Minor version changes

The following examples identify a minor release:

- Adding a feature.
- Adding, removing, or renaming an input or output variable
- Changing the default value of an input variable

    A change to a default value might be considered a major version change if it affects infrastructure that is deployed in the previous version.
- Adding or removing allowable values to input variables
- Requiring a new Terraform provider
- Updating the required provider version constraints

If we anticipate that a minor version change is likely to require code changes by consuming developers, we document the changes in the GitHub release notes.

## Patch version changes

Patches are added to the current release, regardless of the version that they are found in. In other words, if a bug is found in release `X.Y.Z` and the current release is `A.B.C`, the patch is delivered in release `A.B.(C+1)`, not in `X.Y.(Z+1)`.

The following examples identify a patch release:

- Bug fixes
- Dependency updates

    However, if the dependency update exposes a new feature, the release is marked as a minor version.

## Upgrading

When you upgrade from a version `A` to a version `B`, apply each update between `A` and `B`. Although you might successfully upgrade if you skip patch releases in a minor release, that path is not verified with the automatic tests.

## Staying current

Use the most recent module release, if possible. You can use tools such as [Renovate](https://docs.renovatebot.com/) or [Dependabot](https://docs.github.com/en/code-security/dependabot) to help automate the process of updating dependency versions.
