[[_TOC_]]

# Creating Pull Requests

Creating Pull Requests is a staple of using git as a source control. You will need to create a pull request from your feature branch into the dev branch when your feature is complete and so your code can be reviewed.
In order to create a pull request, follow these steps:

![image.png](/.attachments/image-193d3e39-7288-44d0-b68b-a08bcda13be4.png)
1. Go to the Branches screen of the project VSTS page. You can find this under Code -> Branches.
1. Find your feature branch and either right click or left click the ellipsis (…)
1. Select “New pull request”
![image.png](/.attachments/image-e172a786-7ace-4ec0-8a5f-8c211f910cf1.png)
1. Verify that both dropdowns at the top have the correct information. It show read [feature branch] into [dev] (or branch you want your code changes to be merged into)
1. The title and description should make it as clear as possible what the purpose of this merge request is.
1. You can optionally add a work item from here as well.
1. When satisfied, click Create.
1. Once completed the approval process will begin with peer reviews from other developers and any automated build processes in place.

# Setting Autocomplete
![2019-02-13_12-25-28.png](/.attachments/2019-02-13_12-25-28-0c254f22-506e-4463-a3e1-4df50d639394.png)
1. When creating a PR, set the auto complete options to `delete` and `squash`. These options will automatically delete your old branch when  the PR is complete.
1. No additional work should be done in the PRs branch once a PR is submitted unless it is to correct a comment, or build issue. Create a new branch after a PR is submitted.