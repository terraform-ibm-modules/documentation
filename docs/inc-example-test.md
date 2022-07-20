1.  Set the following environment variables:
    - `IC_API_KEY` or `TF_VAR_ibmcloud_api_key`: An IBM Cloud API key for the account that the test uses to provision resources.
    - (Optional) `DO_NOT_DESTROY_ON_FAILURE`: Set this variable to `true` if you do not want to destroy resources when the test fails.
    - (Optional) `FORCE_TEST_REGION`: By default the tests select a region to provision resources in based on current region availability. This variable can be used to force a specific region, if required.
1.  Run the tests:

    - To run all tests:
        ```bash
        make run-tests-local
        ```

    - To run a specific test or tests, use the `RUN` variable to pass a regular expression that matches the names of the tests that you want to run:

        ```bash
        make run-tests-local RUN=TestRunDefaultExample
        ```

If the tests run successfully, you see a `PASS` statement. The tests run the Terraform `init`, `plan`, and `apply` commands, runs a consistency check to make sure that the module is idempotent, and then destroys the resources.
