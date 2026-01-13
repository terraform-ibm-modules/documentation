# Deprecation Policy

A module may be deprecated for several reasons. For example, there might be a newer module available for migration, or one of the IBM Cloud services that the module provisions might have reached its end of life. The following sections describe the phases of the deprecation process:

## Initial Deprecation (90 Days)
A new patch version of the module will be released with the following updates:

- A **deprecation banner** added to the top of the `README.md` file, including the end-of-support date (90 days after the patch release). The banner will also provide details on why the module is deprecated and may include links to alternative modules or migration guides.
- A **warning message** added to the Terraform log output with deprecation details.

During this phase, the module remains maintained and supported; however, no new enhancements will be accepted.

## End of Support – Module Archived

After the 90-day deprecation period, the module will be archived and no longer maintained. Previous versions will remain available for consumption, but there will be no further support or updates. The repository will be archived in a read-only state.
