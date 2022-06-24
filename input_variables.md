# Module inputs

Input variables serve as parameters for a Terraform module, allowing aspects of the module to be customized without altering the module's own source code, and allowing modules to be shared between different configurations.

## Declaring an Input Variable

Each input variable accepted by a module must be declared using a variable block:

```
variable "bucket_name" {
    description = "Name of the bucket"
    type        = string
}
```

The label after the variable keyword is a name for the variable, which must be unique among all variables in the same module. This name is used to assign a value to the variable from outside and to reference the variable's value from within the module.

## Access input variables

Within the module that declared a variable, its value can be accessed from within expressions as var.<NAME>, where <NAME> matches the label given in the declaration block:

```
resource "ibm_cos_bucket" "testBucket" {
  bucket_name          = var.bucket_name
}
```

## When to use `input.tfvars` file

The type argument in a variable block allows you to restrict the type of value that will be accepted as the value for a variable. The type constructors allow you to specify complex types such as collections:

* list(<TYPE>)
* set(<TYPE>)
* map(<TYPE>)

If we want user to pass the complex variable values such as above, then use `input.tfvars`

## Example

Say to provision a multi-zone cluster, we define a variable of type map as follows:

```
variable "worker_zones" {
    type = map
    description = "List of worker zones to attach"
}
```

and define the values in `input.tfvars` as follows:

```
worker_zones = {
    dal12 = {
      public_vlan = "2944984"
      private_vlan = "2944986"
    }
    dal10{
        public_vlan = "2944963"
        private_vlan = "2944964"
    }
}

```

## How to pass `input.tfvars` to module

To review the plan for the configuration defined (no resources actually provisioned)

```
terraform plan -var-file=./input.tfvars
```

To execute and start building the configuration defined in the plan (provisions resources)

```
terraform apply -var-file=./input.tfvars
```

To destroy the VPC and all related resources

```
terraform destroy -var-file=./input.tfvars
```