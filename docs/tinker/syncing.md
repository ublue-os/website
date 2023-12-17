# Keeping your fork in sync

The `ublue-os/startingpoint` repository occasionally receives updates, often bug fixes or new features. This guide is useful when you want to receive the benefits of our ongoing development process. However, this is mostly generally applicable and useful even when your repository is not based on `ublue-os/startingpoint`.

There are many equal ways to do this, but this guide will cover an easy way that you can do entirely in GitHub's web interface.

1. If your fork has a branch called `template`, delete it. Then create a new branch called `template` and choose the source to be `ublue-os/startingpoint`'s `template` branch.
2. Create a new pull request on your repo. Choose the base to be the `live` branch on your repo, and the head to be the newly created `template` branch.
3. If there are merge conflicts, you can resolve them in the GitHub web UI. If you had attempted to do the merge directly from the upstream, this would not be possible.
4. Merge using a merge commit, not a squash merge. If you use a squash merge, GitHub won't know that your repo has synced up.

If you wish to automate the creation of the PRs, you can set up [wei/pull](https://wei.github.io/pull/) on your repo.