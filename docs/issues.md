# Known issues

The following open issues might affect your modules.
## Autoscaling issue with IBM Cloud Databases (ICD) and v1.50 of the IBM Cloud Provider

You receive a failure when you try to deploy any IBM Cloud Databases (ICD) module that includes the autoscaling block and uses IBM Cloud Provider version 1.50 or later.

### Why it's happening

An issue exists with the IBM Cloud Provider version 1.50 around autoscaling. For more information about the issue, see [4339](https://github.com/IBM-Cloud/terraform-provider-ibm/issues/4339) in the IBM Terraform Provider GitHub repo.

### How do I solve this problem?

If you experience the issue with autoscaling, make sure that you are running the most recent version of the module.

If you continue to see the issue with the most recent version of the module, change your Terraform code:

- Set the `IBM-Cloud/ibm"` provider to use only [version 1.49](https://github.com/IBM-Cloud/terraform-provider-ibm/releases/tag/v1.49.0).
- Make sure that properties that are passed from your deployment to the ICD module are not set to null or empty values.
