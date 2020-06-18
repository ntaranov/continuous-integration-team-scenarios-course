## An Error was Found in Production

They say "testing can be used to show the presence of bugs, but never to show their absence." Even though we had some tests and they didn't show us any bugs, a sneaky bug made it into production.

In a scenario like this we need to take care of:
  - whatever deployed into production;
  - the code in `master` branch with the bug, which might be used to start new work.

### Rolling Back vs Fixing Forward

"Rolling back" is deploying a known good previous version to production and reverting the code changes containing bug. "Fixing forward" is adding the fix to `master` and deploying a new version as soon as possible. With continuous delivery and good test suite in place, because APIs and database schemes change as code deployed to production production, rolling back is generally much harder and riskier than fixing forward. 

Because reverting does not bring any risk at all for us, we are going the "revert" way to simulate situation when we
- fix the production ASAP;
- make the code in `master` immediately suitable for starting new work.

### ⌨️ Activity

1. Checkout `master` branch locally.
1. Pull the latest changes form the remote.
1. Revert the merge commit of [{{ prTitle }}]({{ prUrl }}) PR in `master`.
1. Push to remote.

<details><summary>Show the commands...</summary>

```bash
# Checkout master branch locally.
git checkout master

# Pull the latest changes form the remote.
git pull

# Revert the merge commit of {{ prTitle }} PR in master.
# We are reverting merge commit, so we need to indicate which line we choose to remain
git show HEAD

# let's suppose, the previous master branch tip commit listed first by the previous command
git revert HEAD -m 1
# you can leave the standard commit message

# Push to remote.
git push
```
</details>

I will answer here after changes to master are reverted.
