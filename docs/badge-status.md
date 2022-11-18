# Badges for modules

You can tell at a glance the stage of development and approval of a IBM Cloud Terraform module by checking the status badge in the main readme file in the repository. You can also see the modules that are publicly available in the IBM Cloud Catalog.

## Status badges
The readme file for the module in GitHub includes a status badge.

### Active statuses
The following status badges are supported for active modules. The order follows the typical development stages for modules.

1.  ![Incubating (Not yet consumable)](https://img.shields.io/badge/status-Incubating%20(Not%20yet%20consumable)-red)

    - The module is in early stage and is not yet consumable.

    <details>
      <summary>Markdown (incubating)</summary>

      ```md
      [![Incubating (Not yet consumable)](https://img.shields.io/badge/status-Incubating%20(Not%20yet%20consumable)-red)](https://terraform-ibm-modules.github.io/documentation/#/badge-status)
      ```
    </details>
1.  ![Implemented (No quality checks)](https://img.shields.io/badge/Status-Implemented%20(No%20quality%20checks)-yellowgreen)

    - The module is in advanced development, which indicates that it is valuable to consumers. The module does not yet have quality checks in place.

    <details>
      <summary>Markdown (implemented)</summary>

      ```md
      [![Implemented (No quality checks)](https://img.shields.io/badge/Status-Implemented%20(No%20quality%20checks)-yellowgreen)](https://terraform-ibm-modules.github.io/documentation/#/badge-status)
      ```
    </details>
1.  ![Stable (With quality checks)](https://img.shields.io/badge/Status-Stable%20(With%20quality%20checks)-green)

    - The module is reviewed and approved by the project maintainers. Quality checks are run against the code. The module is supported by the IBM Cloud Terraform modules community.

    <details>
      <summary>Markdown (stable)</summary>

      ```md
      [![Stable (With quality checks)](https://img.shields.io/badge/Status-Stable%20(With%20quality%20checks)-green)](https://terraform-ibm-modules.github.io/documentation/#/badge-status)
      ```
    </details>
1.  ![Graduated (Supported)](https://img.shields.io/badge/Status-Graduated%20(Supported)-brightgreen)

    - The module is reviewed, approved, and supported by IBM.

    <details>
      <summary>Markdown (graduated)</summary>

      ```md
      [![Graduated (Supported)](https://img.shields.io/badge/Status-Graduated%20(Supported)-brightgreen)](https://terraform-ibm-modules.github.io/documentation/#/badge-status)
      ```
    </details>

### Other statuses

- ![Inactive](images/badge-inactive.svg "Inactive")
    - This module is no longer maintained or is deprecated, and might be archived. Do not use.

## Release badges

- ![latest SemVer release](images/badge-release.svg "latest SemVer release")
    - Latest semantic versioning release of the module in GitHub.
- ![latest SemVer release](images/badge-release-cloud.svg "Catalog release")
    - This module is available in the IBM Cloud catalog.
