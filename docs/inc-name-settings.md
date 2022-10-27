To help make sure that the repo name and description are not changed except through pull requests, they are defined in the `settings.yml` file.

Check to make sure that values are uncommented and correct:

1.  Open the `.github/settings.yml` file.
1.  If not already updated, uncomment the `name` and `description` properties and set the values to what you specified when you requested the repo, as in the following example.

    ```yaml
    repository:
      # Update the name and description to match your repo
      name: "terraform-ibm-activity-tracker"

      description: "Installs Activity Tracker into an IBM Cloud account"
    ```
