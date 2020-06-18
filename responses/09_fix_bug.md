## Fix CI list and return it to master

We reverted `{{ firstBranchName }}` merge entirely. Good news is that now we don't have the bug in `master`. Bad news is that our precious continuous integration list is gone too. So, ideally we need to apply fix over commits from `{{ firstBranchName }}` and return them to `master` along with the fix.

We can approach the task differently:
- revert the commit which reverts the merge of `{{ firstBranchName }}` to `master`;
- cherry-pick commits from the former `{{ firstBranchName }}`.

Different teams use different approaches, and we will cherry-pick the commits into a separate branch and will create a separate pull request for the new branch.

### ⌨️ Activity

1. Create a branch called `{{ featureFixBranchName }}` and checkout it.
2. Cherry-pick all the commits of the former `{{ firstBranchName }}` into the new branch. Resolve the merge conflicts.
3. Add the regression test to `ci.test.js`:
    ```js
    it('does not contain the sneaky bug', () => {
      expect( /.*sneaky\s+bug.*/gi.test(fileContents)).toBe(false);
    });
    ```
4. Run tests locally to make sure they don't pass.
5. Delete text " with a sneaky bug" in `ci.md`.
6. Add the changes to tests and to the steps list and commit them.
7. Push the branch to remote.


<details><summary>Show the commands...</summary>

```bash
# Create a branch called {{ featureFixBranchName }} and checkout it.
git checkout -b {{ featureFixBranchName }}

# Cherry-pick all the commits of the former {{ firstBranchName }} into the new branch.
# use log to figure out hashes for the commits
# - preceding one adding the first list items: C0
# - adding the last items to list: C2
git log --oneline --graph
git cherry-pick C0..C2
# resolve the merge conflicts like you did merging feature-steps into master
# - edit ci.md and/or ci.test.js
# - add the files to index
# - run "git cherry-pick --continue", you can leave the commit message

# Add the regression test to ci.test.js
# Run tests locally to make sure they don't pass.

# Delete text " with a sneaky bug" in ci.md.

# Add the changes to tests and to the steps list and commit them.
git add ci.md ci.test.js
git commit -m "Fix the bug in steps list"

# Push the branch to remote.
git push --set-upstream origin {{ featureFixBranchName }}

```
</details>