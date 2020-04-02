#Work Item Status Flow

![work item status.png](/.attachments/work%20item%20status-25e9cf72-e3b1-4e46-8ace-8855eea24a38.png)

1. **New**: Work Items should live in this status until it has been verified by the 
leadership team.
1. **Assigned To Developer**: Work Item is ready to be worked on and is assigned to a developer and a sprint.
1. **Dev Work Started**: Developer is actively working on the item.
   * In the event that a developer doesn't have enough information or cannot reproduce an issue, they should leave a comment on the task tagging whoever is needed to participate in the discussion. Those involved should assist in moving the item out of this state as soon as possible.
1. **Code Complete**: This is an automated status change after a PR has been submitted.
1. **Deployed To Dev**: This is an automated status change after the PR has been approved and has been deployed to the dev environment.
1. **Verified In Dev**: The developer has checked everything still works in the dev environment
1. **Deployed to QA**: This is an automated status change:
   * The Dev branch has been promoted to qa.
   * QA has confirmed they are ready to receive new changes.
   * "qa" branch has been deployed to the qa environment.
1. **Assigned to QA**: QA Lead has delegated the work item.
1. **QA Work Started**: QA member is validating the task.
1. **Closed/Rejected**: QA has either passed or failed the changes.
   * If the task is rejected, it should be reassigned to the developer. From there the developer to verify the rejection and work with QA and Lead if necessary to address any concerns
   * If the task is approved it will be marked "Closed"