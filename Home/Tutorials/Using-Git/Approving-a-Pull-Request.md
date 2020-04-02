# Approving a Pull Request

Code should be subject to peer reviews when possible. This article will show how to review Pull Requests (PR) in TFS using Git.

To begin, navigate the PR in need of review. This can be found under Project -> Code -> Pull Request. You may have to navigate to the “Active” tab. Then click the PR in need of review.

The PR screen will be shown. Take notice of the following items:
![image.png](/.attachments/image-103ec1bc-edb1-4586-b096-f87f9163774e.png)

1. Some branches (dev, stag, master) will have Policies in place and the PR must conform to these policies in order for the PR to merged and completed.
   * Notice in this example that there is a requirement to have a certain number of reviews approval. This insures that at least one other person has reviewed and acknowledge the changes that are about to be received.
    * This example also has a required reviewer, this will often be the Team Lead/Architect. The lead should be a required reviewer when promoting code changes to any protected branch.
1. The files tab shows a file diff report from the check in
1. When ready to approve or reject the PR click the arrow to get a list of possible actions.
1. When the final approval has been made and the PR is ready for promotion, click “Complete” or the drop down arrow for more options.

## Approval Actions
![image.png](/.attachments/image-37b9f0e0-5eac-4407-b74d-4772aa53825c.png)
The Approval Actions provide the review with options to indicate the readiness of the PR.

## Completion Actions
![image.png](/.attachments/image-2b323464-a506-44cc-aa9b-c7b8b4ceec03.png)
The Completion Actions provide both the Reviewer and the PR originator with some additional options.
1. Notice that all of the policy requirements have now been met and the PR can be merged.
1. The originator can setup some default when the PR is approved. For instance auto delete the feature branch (4).
1. If tasks are linked in the check-in comments or work items added, merging the PR can automatically set the status of these work items to Complete
1. It is recommend to delete the server side feature branch when merging. This keeps the code tree clean of work that has already been completed. If new work is need to a task after the merge, a new ticket should be created or the original ticket should be reopen and the developer should rebranched from dev.
1. Clicking “Complete merge” will performed the actions as indicated above, close the PR, and merge the code into the desired branch.
