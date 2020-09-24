# Module outputs

Output values are like the return values of a Terraform module, and have several uses:

* A child module can use outputs to expose a subset of its resource attributes to a parent module.
* A root module can use outputs to print certain values in the CLI output after running terraform apply.

## Declaring an output block

Each output value exported by a module must be declared using an output block:

```
output "cos_instance_id" {
  description = "The ID of the cos instance"
  value       = ibm_resource_instance.cos_instance.id  
}
```

Since, the output values of a module are part of its user interface, you can briefly describe the purpose of each value using the optional description argument:

The label immediately after the output keyword is the name, which must be a valid identifier. In a root module, this name is displayed to the user; in a child module, it can be used to access the output's value.

The value argument takes an expression whose result is to be returned to the user. In this example, the expression refers to the `id` attribute exposed by an `ibm_resource_instance` resource defined elsewhere in this module (not shown). Any valid expression is allowed as an output value.

## Accessing Child Module Outputs

In a parent module, outputs of child modules are available in expressions as module.<MODULE_NAME>.<OUTPUT_NAME>. For example, if a child module named `cos` declared an output named `cos_instance_id`, you could access that value as module.cos.cos_instance_id.

## Usage

```
module "cos" {
  source = "../../modules/cos_instance"

  service_name         = var.service_name
  resource_group_id    = data.ibm_resource_group.cos_group.id
  plan                 = var.plan
  region               = var.region
}

module "cos_bucket" {
  source = "../../modules/cos_bucket"

  bucket_name          = var.bucket_name
  cos_instance_id      = module.cos.cos_instance_id  
  location             = var.location
  storage_class        = var.storage_class

}
```
