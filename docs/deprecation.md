# Deprecation process

A module may become deprecated for a number of reasons. For example there might be a replacement module to migrate to, or perhaps one of the IBM Cloud services that the module provisions is end of life. Below lists the different phases of the deprecation process:

## Initial deprecation (90 days)
A new patch version of the module will be released with the following:
- A deprecation banner at the top of `README.md` file which includes an end of support date. That date will be 90 days after the patch version is released. This banner will also include more details about why the module is deprecated and may link to alternative modules or migration guides.
- A warning added to the terraform log output with deprecation details.

The module is still maintained and supported while in this deprecation phase, however new enhancements will not be accepted into the module.

## End of support - module archived
After the 90 day deprecation period, the module will be archived and no longer maintained. Previous versions of the module will still remain consumable, but there will no longer be any support or further updates to the module as the repository itself will be archived, making it read-only.
