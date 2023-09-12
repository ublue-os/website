# Automatic setup using the command line

<video controls="true" allowfullscreen="true">
    <source src="https://user-images.githubusercontent.com/60004820/252016808-4ebe18a2-6bdb-43cb-b2b6-407f62ad1b78.mp4" type="video/mp4">
</video>

For automatic setup using the command line, there is a community-built tool called [`create-ublue-image`](https://github.com/xynydev/create-ublue-image). The tools uses `github-cli` which technically has a lot more access to your GitHub account than needed, if this is a concern to you, you can read the source code. It is packaged as a container you can run with [Podman](https://podman.io/), which is installed by default on Universal Blue images.

1. Run the command `podman run -v "$(pwd)":/host --security-opt label=disable -it ghcr.io/xynydev/create-ublue-image` in a subdirectory of your home directory
    - This will mount the current directory for modification inside the container. If you want the folder containing your repo to be in a certain directory like `~/dev`, you should `cd` into that before executing the tool.
    - If you have any issues, read [the project's](https://github.com/xynydev/create-ublue-image) README and submit to its issue tracker.
2. Follow the instructions the tool gives you

> !!! note
 This tool currently does not fork the `ublue-os/startingpoint` repository. This will slightly complicate syncing with upstream.

## Syncing

In order to sync new changes from the upstream template, run the following commands:

```bash
# Retrieve latest changes from upstream's template.
git fetch upstream template
git checkout template
git merge --ff-only upstream/template
git push

# Rebase your own "live" changes onto the latest template.
git checkout live
git rebase --onto live template

# Perform a force-push to update your "live" branch on GitHub, to deploy.
# The "lease" ensures that you won't overwrite "live" if GitHub's version
# is different than your local version (ie. if a team member pushed to it).
git push --force-with-lease
```

Most of the time, the rebased changes will be applied automatically without any need for manual editing. However, if you've modified any core files from the template, then you might have merge conflicts which need to be manually resolved. It's therefore recommended that you use a GUI such as [GitHub Desktop](https://desktop.github.com/) to do your rebase in a visual manner, to handle any conflicts.

## SSH

Note that the `create-ublue-image` sets up the "origin" remote to use HTTPS URLs. If you want to connect to GitHub through SSH instead, run the following command to update your local repository's URL:

```bash
git remote set-url origin git@github.com:UserName/RepoName.git
```
