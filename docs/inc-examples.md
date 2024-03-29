Every module must contain at least one example.

- An example is a [root terraform module](https://www.terraform.io/language/modules#the-root-module) that uses the module and demonstrates its usage.
- Examples are located in the `examples` directory. See [module structure](module-structure.md).
- The main readme file includes links to your examples that are created by a pre-commit hook that creates the links.

The following recommendations and good practices might help you structure your examples:

- Make at least one example as simple and basic as possible. For example, call the module with all default input values.
    It is common to name this example `basic`.
- Don't require prerequisites for running the example. If possible, set up all dependencies programmatically as part of the example execution. For example, code an `openshift-vpc-module` example that creates the VPC, and then passes it as an input to the `openshift-vpc-module`.
- Add as many examples as necessary to cover the most common usage scenarios of your module. To keep the example simple to consume and understand, cover only one usage scenario per example.
- Create examples to help developers understand how to consume your module in their Terraform code.
