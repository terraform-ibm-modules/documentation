# Release versioning

Modules are updated regularly. The changes adhere to [semantic versioning](https://semver.org/), with releases labeled as `{major}.{minor}.{patch}`. [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) are used to identify module versions.

Release levels apply to both modules and submodules. For example, a major version change to a submodule results in a major release for the whole module. However, changes to examples do not drive release levels, unless the example is published as a Deployable Architecture to the IBM Cloud.

## Determining version updates

No universal criteria exist to determine terraform module versioning. However, when we evaluate changes, we consider major version updates only necessary when any of the actual infrastructure that is deployed by the module will either be destroyed or modified in a way that may affect every day operations.

### Major version changes

A major version release is one that impacts the actual infrastructure that is deployed by the module itself. The following are example of major version updates:

- Adding changes that may destroy infrastructure or update resources (that may impact every day operations) that were created in the previous version
  - Manual steps are documented as GIT release notes with the major version either to avoid ending up in this situation (for example, migrating Terraform state) or to describe a path for business continuity.

### Minor version changes

The following examples identify minor version changes:
- Adding a new feature
- Adding, removing or renaming an input or output variable
- Changing the default value of an input variable (NOTE: This may be a major version change if it impacts already deployed infrastructure)
- Reducing or expanding possible values for input variables
- Requiring a new terraform provider
- Updating the required provider version constraints

As some of the above types of changes could require consuming client developers to update code in order to consume the new minor version, such changes are documented in the versioning GIT release notes

### Patch version changes

## Where patches are added

Patches are added to the current release, regardless of the version that they are found in. In other words, if a bug is found in release `X.Y.Z` and the current release is `A.B.C`, the patch is delivered in release `A.B.(C+1)`, not in `X.Y.(Z+1)`.

The following examples identify patch version changes:
- Bug fix
- Dependency update (unless dependency is exposing a new feature, in which case a minor version release would be done)

## Upgrading

When you upgrade from a version `A` to a version `B`, it is recommended to apply each update between `A` and `B`. Although you might successfully upgrade if you skip patch releases in a minor release, that path is not verified with the automatic tests.

## Staying current

Use the most recent module release, if possible. You can use tools such as [Renovate](https://docs.renovatebot.com/) or [Dependabot](https://docs.github.com/en/code-security/dependabot) to help automate the process of updating dependency versions.
