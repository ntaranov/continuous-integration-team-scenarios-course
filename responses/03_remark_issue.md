## Add remark about the CI steps being opinionated

The list used in this course is opinionated, we should add a remark stating this.


### ⌨️ Activity: Create a pull request for the remark

1. Check out `master` branch.
2. Create a branch named `{{ remarkBranchName }}`.
3. Add the remark text at the bottom of `ci.md`.
  ```
  > **GitHub flow** is sometimes used as a nickname to refer to a flavor of trunk-based development  
    when code is deployed straight from feature branches. This list is just an interpretation  
    that I use in my [DevOps courses](http://redpill.solutions).  
    The official tutorial is [here](https://guides.github.com/introduction/flow/).
  ```
4. Commit the changes.
5. Push branch `{{ remarkBranchName }}` to the remote.
6. [Open a pull request]({{ createPrUrl }}) named **{{ remarkPrName }}** with head branch `{{ remarkBranchName }}` and base branch `master`.

<details><summary>Show the commands...</summary>

```bash
# Check out master branch. Create a branch named {{ remarkBranchName }}.
git checkout master

# Create a branch named bugfix-remark.
git checkout -b {{ remarkBranchName }}

# Add the remark text at the bottom of ci.md.

# Commit the changes
git add ci.md
git commit -m "Add remark about the list being opinionated"

# Push branch {{ remarkBranchName }} to the remote.
git push --set-upstream origin {{ remarkBranchName }}

# Open a pull request using GitHub UI as described above
```
</details>
