## Merge Conflict

Even though we didn't do anything wrong, and tests pass for our code, we still cannot merge branch `{{ firstBranchName }}` into master. This is because another branch `{{ remarkBranchName }}` was merged into `master` as we were working on the pull request.
This creates situation when remote `master` branch has commits newer than the one we based branch `{{ firstBranchName }}` on. Because of this, we cannot just add commits from `{{ firstBranchName }}` to `master` and fast-forward `master` HEAD to the tip of `{{ firstBranchName }}`. In this situation we need to either merge or rebase `{{ firstBranchName }}` on master. GitHub can actually perform automatic merge if there is no conflicts. Alas, in our situation both branches have concurrent changes to file `ci.md`, a situation known as merge conflict, and we need to resolve it manually. To make history compatible with the remote `master` branch, we can both merge `{{ firstBranchName }}` into `master` or rebase it on `master`.

<details><summary>More about merge and rebase</summary>

### Merge

- Creates an extra merge commit and preserves work history
  - Contains initial head branch commits with original timestamps and authors
  - Preserves commit SHAs and references to them in pull requests discussion  
- Requires resolving conflicts just once 
- Makes history non-linear
  - History might be hard to read because of lots of branches (think IDE cable)
  - Makes automatic debugging harder, e.g., makes `git bisect` less useful - it's only going to find a merge commit

### Rebase

- Replays commits from head branch on top of base branch one-by-one
  - New commits with new SHAs are formed resulting in the commits being linked to original pull requests but not to the relevant comments
  - Commits might be recombined and amended in the process or squashed into fewer, even into just one commit
- Might require resolving a number of conflicts 
- Supports linear history
  - Might be easier to read if not too long without a good reason
  - Auto debugging and troubleshooting is somewhat easier: supports `git bisect`, might make automatic rollbacks more granular and predictable 
- Requires force pushing the rebased head branch when used with pull requests

Usually, teams agree to employ the same strategy anytime they need to merge changes. It can be "pure" merge or rebase or somethings in-between like doing interactive rebase locally for the branches not published to remote, but merges for "public" branches. 

</details>

We'll use merge here.

### ⌨️ Activity

1. Make sure latest code is pulled to local `master` branch.
1. Check out branch `{{ firstBranchName }}`.
1. Merge `master` branch into it. A merge conflict related to concurrent changes to `ci.md` will be reported.
1. Resolve the conflict so that both our CI list and the remark about it remain.
1. Push the merge commit into remote `{{ firstBranchName }}`.
1. Check the pull request status in GitHub UI, wait until the merge is permitted.
1. Merge the pull request using GitHub UI. When asked about it, delete `{{ firstBranchName }}` branch.


<details><summary>Show the commands...</summary>

```bash
# Make sure latest code is pulled to local `master` branch
git checkout master
git pull

# Check out branch {{ firstBranchName }}
git checkout {{ firstBranchName }}

# Merge master branch into it
git merge master

# A merge conflict related to concurrent changes to ci.md will be reported
# => Auto-merging ci.md
#    CONFLICT (content): Merge conflict in ci.md
#    Automatic merge failed; fix conflicts and then commit the result.

# Resolve the conflict so that both our CI list and the remark about it remain.
# edit ci.md so that it doesn't contain the merge confilict markers
git add ci.md
git merge --continue
# you can leave the default commit message

# Push the merge commit into remote {{ firstBranchName }}.
git push

# Check the pull request status in GitHub UI, wait until the merge is permitted.
# Merge the pull request using GitHub UI. When asked about it, delete feature-steps branch.
```
</details>