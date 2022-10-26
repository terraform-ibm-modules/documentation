To help make sure that the repo name and description are not changed except through pull requests, add the repo name and description to the repo settings file.

1.  Open the `.github/settings.yml` file.
1.  Set the repo `name` and `description` fields with what you specified when you [requested the repo](#request-a-repo).

    ```yaml
    repository:
      # Update the name and description to match your repo
      name: "terraform-ibm-module-template"
      description: "Template for starting a new module"
    ```
