# Region in Deployable Architecture

Certain deployable architectures allow you to add or remove related or dependant deployable architectures based on your use case. If you have chosen to add deployable architectures that provision other regional services, the value that is select for the parents deployable architecture `region` input will automatically be used for all regional services that are provisioned by the other deployable architectures you have added.

It is possible to explicitly override the region for any of the related or dependant deployable architectures by following these steps:

1.  In the IBM Cloud console, navigate to the project configuration which contains the stacked deployable architectures.
1.  In the row for the deployable architecture that you wish to update the region input for, click the Options icon and select Edit.
1.  Find the `region` input variable and click the "X" to remove the pre-configured reference value. From the dropdown, select the desired region.
1.  Click Save.
1.  Proceed with validation and deployment.
