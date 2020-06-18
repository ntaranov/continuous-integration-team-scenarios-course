## Continue working and adding tests

Collaborating on a pull request often results in additional work being requested. Usually, this is a result of a review or a discussion, but for our course, we are going to simulate this by adding another item to our CI checklist.

Some test coverage is usually in place to support Continuous Integration. The tests coverage requirements differ and are usually found in a document like "contribution guidelines". We are going to be straightforward and will add a test for each line in our checklist.

When working through the activity part, first try to commit tests. If you installed the `pre-commit` hook correctly earlier, the test we've just added will fail and nothing will be committed. Please note that that this is how we know that our tests actually check something. Curiously, if we started with the code before tests, tests passing could mean either that the code works as expected or that the tests don't really check anything. Also, if we didn't write tests first, we could forget writing them completely, as nothing would remind us about it.

<details><summary>Test Driven Development (TDD) advocates writing tests before code.</summary>
Usual TDD work process looks like this.

1. Add a test.  
2. Run all tests and see if the new test fails.  
3. Write the code.  
4. Run tests.  
5. Refactor code.  
6. Repeat.  

Because not passing tests are usually displayed in red, and passing displayed in green, the cycle is also known as "red-green-refactor".

</details>

After letting the tests fail attempting to commit them, add and commit the actual checklist text. You will see that tests are passing ("green").
Then, push the new code to the remote and see how tests are run in the pull request and the pull request's status is updated.


### ⌨️ Activity

1. Checkout branch `{{ firstBranchName }}`.
2. Add the following tests to `ci.test.js` after the last `it(...);` call.
  ```js
    it('5. Merge/rebase commits from master. Make tests pass on the merge result.', () => {
      expect(/.*merge.*commits.*tests\s+pass.*/ig.test(fileContents)).toBe(true);
    });

    it('6. Deploy from the feature branch to production.', () => {
      expect(/.*Deploy.*to\s+production.*/ig.test(fileContents)).toBe(true);
    });

    it('7. If everything is good in production for some period of time, merge changes to master.', () => {
      expect(/.*merge.*to\s+master.*/ig.test(fileContents)).toBe(true);
    });
  ```
3. Try to commit the tests. If the `pre-commit` hook is in place, the commit will fail.  
4. After, add this text to `ci.md`.
  ```
  5. Merge/rebase commits from master. Make tests pass on the merge result.  
  6. Deploy from the feature branch with a sneaky bug to production.
  7. If everything is good in production for some period of time, merge changes to master. 
  ```
5. Add and commit the changes locally.
6. Push the changes to `{{ firstBranchName }}` branch.


<details><summary>Show the commands...</summary>

```bash

# Checkout branch {{ firstBranchName }}
git checkout {{ firstBranchName }}

# Add tests to ci.test.js as described above

# we add ci.test.js to commit it later
git add ci.test.js

# Try to commit the tests. If the pre-commit hook is in place, the commit will fail.
git commit

# After, add text to ci.md as described above

# Add and commit the changes locally
git add ci.md
git commit -m "Add the remaining CI steps"

# Push the changes to {{ firstBranchName }} branch.
git push

```

</details>


