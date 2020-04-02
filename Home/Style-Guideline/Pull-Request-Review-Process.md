1. Check PR for basic easy to identify "code smell" issues such as javascript equality (e.g. `==` vs `===`).
1. After a visual inspection and:
   - A knowledge gap issue such as originators unfamiliarity with a code section where "dev2" might know that the change will result in the area breaking.
      - Set the PR status to rejected and leave a comment.
   - A knowledge gap issue where the originator has used either an incorrect method or code will result in a exception:
      - Set the PR status to rejected and leave a comment.
   - A firm code style guideline rule has been broken
      - Set the PR status to rejected and leave a comment with a link to related guide.
   - A code migration is required (e.g. from select box to an appropriate select component)
      - Set the PR status to rejected and leave a comment.
   - A question or comment about the validity of a change
      - Set the PR status to "Waiting for author" and leave a comment.
1. If a glancing review reveals no immediate issues, begin in depth review:
    1. Pull the PR branch down.
    1. Perform a fresh build in visual studio.
    1. Perform a fresh build of angular code.
    1. Clear the "lookup" table in indexed db.
    1. **REFRESH**. Make sure to refresh the browser window and verify the new code has been loaded by examing the sources in Chrome
    1. Navigate to the appropriate section.
    1. Verify no breaking changes along the way.
    1. Verify PR resolves attached tickets.
    1. If/When applicable, run UI automation test suite.
1. Based on the findings of the in depth review
   - Mark PR as approved
   - or mark PR as rejected and provide a comment.