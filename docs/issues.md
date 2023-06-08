# Known issues

The following open issues might affect your modules.

## No support in IBM Console CBR UI for access tags

You cannot create or update access tags for resources when you create or update a [context-based restriction (CBR) rule](https://cloud.ibm.com/context-based-restrictions/rules) in the IBM Cloud console UI.

### Why it happens

The CBR UI in the IBM Cloud console does not support creating or editing rules with tags.

### How do I solve this problem?

To change the tag in a CBR rule, edit the rule outside the UI. For example, see the Terraform [documentation about tags](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cbr_rule#tags) in `ibm_cbr_rule`.
