# Contributing to IBM Cloud Terraform Modules




Following these contribution guidelines helps to communicate that you respect the time of the developers managing. In return, they should reciprocate that respect in addressing your issue, assessing changes, and helping you finalize your pull requests.

The process described here has several goals:

- Maintain IBM Cloud Terraform Modules quality
- Fix problems that are important to users
- Engage the community in working toward the best possible IBM Cloud Terraform modules

Please ensure following steps:

1. Fork the project, clone your fork, and configure the remotes:

   ```bash
   # Clone your fork of the repo into the current directory 
   git clone https://github.com/<your-username>/<repo-name>
   
   # Navigate to the newly cloned directory
   cd <repo-name>
   
   # Assign the original repo to a remote called "upstream"
   git remote add upstream https://github.com/<upstream-owner>/<repo-name>
   ```

2. If you cloned a while ago, get the latest changes from upstream:

   ```bash
   git checkout <dev_branch>
   git pull upstream <dev_branch>
   ```

3. Create a new topic branch (off the main project development branch) to contain your feature, change, or fix:

   ```bash
   git checkout -b <topic-branch-name>
   ```

4. Commit your changes in logical chunks. Use Git's [interactive rebase](https://help.github.com/articles/interactive-rebase)
   feature to tidy up your commits before making them public.

5. Locally merge (or rebase) the upstream development branch into your topic branch:

   ```bash
   git pull [--rebase] upstream <dev-branch>
   ```

6. Push your topic branch up to your fork:

   ```bash
   git push origin <topic-branch-name>
   ```

7. Open a pull request with a clear title and description.

8. Make sure the github workflows are succefully running over the PR.

**IMPORTANT**: By submitting a patch, you agree to allow the project owner to
license your work under the same license as that used by the project.

NOTE: Be sure to merge the latest from "upstream" before making a pull request!

For more info [refer](https://github.com/terraform-ibm-modules/terraform-ibm-issue-tracker/blob/main/README.md).