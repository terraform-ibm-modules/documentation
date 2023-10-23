Run your examples to test the logic. After the examples run, destroy the resources.

1.  Set the `ibmcloud_api_key` environment variable that the test uses.

    ```bash
    export TF_VAR_ibmcloud_api_key=<YOUR_API_KEY>
    ```

    Replace `<YOUR_API_KEY>` with the value of the API key that you want to use to test the code.

1.  In the `examples/default` directory, initialize the module to pull the dependencies.

    ```bash
    terraform init
    ```

1.  Apply the configuration and run the example.

    ```bash
    terraform apply
    ```

    Confirm that you want Terraform to apply the changes by typing `yes`. If everything runs successfully, you validated your Terraform logic.

1.  Clean up.

    1.  Run the following command to remove the resources that the example created.

        ```bash
        terraform destroy
        ```

    1.  Confirm that you want Terraform the destroy the resources by typing `yes`.
