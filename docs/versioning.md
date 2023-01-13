# Release compatibility

Modules are updated regularly. The changes adhere to [semantic versioning](https://semver.org/), with releases labeled as `{major}.{minor}.{patch}`. [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) are used to identify module versions.

A major release level indicates a change that is not compatible with earlier versions. A minor release includes new capabilities and includes only compatible changes. A patch includes mostly bugs fixes that are compatible with an earlier version.

Release levels apply to both modules and submodules. For example, an incompatible change to a submodule results in a major release for the whole module. However, changes to examples do not drive release levels. So, a minor release to the module might include incompatible changes in example code.

## Determining compatibility

No universal criteria exist to determine compatibility. However, when we evaluate changes, we consider the possible assumptions that client developers might have and that indicate that a particular change is likely not compatible.

### Incompatible changes

At a high level, a change that is incompatible with earlier versions is a change that causes code to stop working or might destroy infrastructure. Sometimes modules require these incompatible changes. Known incompatible changes are introduced only in major releases.

Although it's not possible to identify all cases that might break existing code or destroy infrastructure, the following kinds of changes are considered incompatible with earlier versions:

- Adding changes that destroy infrastructure or update resources that are created in the previous version

    Manual steps are documented with the major version either to avoid ending up in this situation (for example, migrating Terraform state) or to describe a path for business continuity.
- Removing an output variable
- Adding a required input variable with no default value
- Changing the default value of an input variable
- Fixing certain security issues

### Compatible changes

The following examples identify generally compatible changes:

- Adding required input variables with a default value

    A minor version change. Users can consume the module without the new input variable. However, they can optionally use the variable.
- Removing input variables

    A minor version change for new feature. A patch release for a fix.

    To minimize disruption, the Terraform variable remains in the code as optional. A message is returned when users reference the variable to indicate that the variable is deprecated and will be removed in the next major release of the module.
- Reducing or expanding possible values for input variables

## Where patches are added

Patches are added to the current release, regardless of the version that they are found in. In other words, if a bug is found in release `X.Y.Z` and the current release is `A.B.C`, the patch is delivered in release `A.B.(C+1)`, not in `X.Y.(Z+1)`.

## Upgrading

Patches and minor releases are compatible with the current version. You can use a patch or minor release as a drop-in replacement to a release in the same minor branch.

When you move from the current release to the next minor or patch release, that upgrade is compatible with the current release. For example, you can upgrade from release `X.Y.Z` to the next patch release `X.Y.(Z+1)`. Or you can upgrade from release `X.Y.Z` to minor release `X.(Y+1).Z)` if patch `X.Y.(Z+1)` is not already released.

?> **Tip**: When you upgrade from a version `A` to a version `B`, make sure to apply each update between `A` and `B`. Also, although you might successfully upgrade if you skip patch releases in a minor release, that path is not verified with the automatic tests.

## Staying current

Use the most recent module release, if possible. You can use tools such as Renovate or Dependabot to help automate the process of updating dependency versions.
