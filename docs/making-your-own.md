# Making your Own

[Universal Blue](https://universal-blue.org/) is both a collection of native container images based on Fedora and a toolkit for you to make your own.

!!! Note "This is moving fast"

    It's still early in the project's life, we're in need of people to help with these docs, so if you find a problem please consider [submitting a pull request](https://github.com/ublue-os/website) to help us improve.

## Why make your own image?

The concept around image based operating systems balances on the idea that the core image is ready to go, and ideally users don't need to touch it, but we understand that people like to tinker. Instead of layering packages that compromise the integrity of upgrades, we provide the tools for you to make your own image allowing you to have a pristine setup with just the configuration you want with minimal maintenance.

## Automatic setup 

You can quickly set up a GitHub repository that builds a native container image based on [ublue-os/startingpoint](https://github.com/ublue-os/startingpoint) using the (experimental) community-maintained [`create-ublue-image`-tool](https://github.com/EinoHR/create-ublue-image).

1. Ensure you have [Podman](https://podman.io/) installed. If you're already using Fedora Silverblue, you should already have it.
2. Run the command `podman run -v "$(pwd)":/host:z -it ghcr.io/einohr/create-ublue-image`
    - This will mount the current directory for modification inside the container. If you want the folder containing your repo to be in a certain directory like `~/dev`, you should `cd` into that before executing the tool.
    - If you have any issues, read [the project's](https://github.com/EinoHR/create-ublue-image) README and submit to its issue tracker.
3. Follow the instructions the tool gives you

In order to update changes from the upstream repository, run the following commands:

```
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

Note that the `create-ublue-image` sets up the "origin" remote to use HTTPS URLs. If you want to connect to GitHub through SSH instead, run the following command to update your local repository's URL:

```
git remote set-url origin git@github.com:UserName/RepoName.git
```

## Manual setup

!!! warning

    Ensure that you are forking the repository and NOT choosing "Use this template". The project moves quickly and it's important for you to get updates! If you want to create multiple repositories (as GitHub doesn't support multiple forks), you have to make sure to keep up-to-date manually.

### Create and configure your repository

1. [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo#forking-a-repository) the [ublue-os/startingpoint](https://github.com/ublue-os/startingpoint) repository on GitHub.
2. Go into the "Settings" tab of your fork at GitHub, and disable the "Template repository" checkbox.
    - Not strictly necessary, but your customized image repo is not a "template" anymore.
3. Create a new branch called `live` based on the `template` branch, and make sure that you only do changes on the `live` branch (you should never modify `template`).
    - The `live` branch is the only branch that will be published to your image container registry. However, all branches will be built, which ensures that other branches and pull requests will still be checked for build errors.
    - You should make the `live` branch your repo's default branch in your GitHub fork's settings.
    - You should periodically sync changes from `ublue-os/startingpoint:template` into your repo's `template` branch. Then, to get the updates into your customized `live` branch, you can either rebase it on top of `template`, or create a merge-commit with the latest changes from `template`. See the "[automatic setup](#automatic-setup)" section for more information about how to perform the syncing and rebasing of your `live` changes, which is the easiest and cleanest way to update yourself to the latest `template` version, since all of your Git commit history will remain clean and logical.
4. Change the image name in [the recipe](https://github.com/ublue-os/startingpoint/blob/template/recipe.yml). Replace the word `startingpoint` with any custom name of your choice. This is what your image will be called when it's uploaded to your container repository.
    - In [ublue-os/main](https://github.com/ublue-os/main), this change is done manually in [the GitHub action](https://github.com/ublue-os/main/blob/main/.github/workflows/build.yml).
5. Ensure that your [GitHub Actions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository) and [GitHub Packages](https://docs.github.com/en/packages) are set up and enabled.
6. [Optional] Install the [Semantic PRs](https://github.com/marketplace/semantic-prs) GitHub app if you want to enforce nice commit messages for your changelogs.

### Set up container signing

Container signing is important for end-user security and is enabled on all Universal Blue images. It is highly recommended you set this up, and by default the image builds *will fail* if you don't.

This part is important, as users must have a method of verifying the image. The Linux desktop must not lag behind in cloud when it comes to supply chain security, so we're starting right from the start! (Seriously don't skip this part) 

!!! warning

    Be careful to *never* accidentally commit `cosign.key` into your git repo.

1. Generate a key pair
    1. Install the [cosign CLI tool](https://edu.chainguard.dev/open-source/sigstore/cosign/how-to-install-cosign/)
        - It's recommended you use [a toolbox](https://universal-blue.org/guide/toolbox/).
    1. Run `cosign generate-key-pair` inside your repo folder
        - Do NOT put in a password when it asks you to, just press enter. The signing key will be used in GitHub Actions and will not work if it is encrypted. 
    1. Add the private key to GitHub
        - If you have the `github-cli` installed, run `gh secret set SIGNING_SECRET < cosign.key`
        - This can also be done manually. Go to your repository settings, under Secrets and Variables -> Actions
        ![image](https://user-images.githubusercontent.com/1264109/216735595-0ecf1b66-b9ee-439e-87d7-c8cc43c2110a.png)
        Add a new secret and name it `SIGNING_SECRET`, then paste the contents of `cosign.key` into the secret and save it. Make sure it's the .key file and not the .pub file. Once done, it should look like this:  
        ![image](https://user-images.githubusercontent.com/1264109/216735690-2d19271f-cee2-45ac-a039-23e6a4c16b34.png)
    1. Add the public key to GitHub
        - Commit the `cosign.pub` file into your git repository
        - In the *Verification* section of `README.md`, change the default image URL to your images URL. This will allow your users to verify the image's signature.

## Modification 

!!! warning "Attention"

    The best place to find information about customizing your image if it's based on the `startingpoint` template is the documentation in the [`README`](https://github.com/ublue-os/startingpoint) and [`recipe.yml`](https://github.com/ublue-os/startingpoint/blob/template/recipe.yml) files.

* Edit `recipe.yml` to modify your image
    - You can configure what packages to install, what to name the image, with more information inside the file
* Add scripts for more in-depth changes that will be executed at the build step. Remember that files cannot be added under `/var`.
* After you've changed a few things and keep an eye on your Actions and Packages section of your repo, you'll generate a new image on every merge and additionally every day. 
* Read the [best practices section](#best-practices) for DOs and DONTs.
* Hang out in the [discussions forums](https://github.com/orgs/ublue-os/discussions) with others to share tips and get help, enjoy!

## Local Testing
see [Local Testing](/local-testing)

## Common Issues found in Testing

- Greetd has SELinux policy issues when trying to install it in `recipe.yml`: [github issue](https://github.com/ublue-os/main/issues/223)
- Installing SDDM the way it is doesn't work as the SDDM user needs to exist: [github issue](https://github.com/ublue-os/main/issues/224)
    - You can get around this by executing `adduser sddm` before running sddm

## Best Practices

The following are some best practices based on experience with learning how to move to this new model:

### What repo to fork?

The instructions here recommend using the [`startingpoint`](https://github.com/ublue-os/startingpoint) template because it:  

- Is made to be modified and customized
- Is more suitable for personal usage
- Has an easier to edit configuration format, YAML, which also supports comments and inline documentation
- Advanced customization can be accomplished at build time by [placing scripts in the appropriate folders](https://github.com/ublue-os/startingpoint/blob/template/scripts/README.md)

Making a custom image by forking a differently structured repository such as [`main`](https://github.com/ublue-os/main) or [`bluefin`](https://github.com/ublue-os/bluefin) might be more appropriate if you intend on having multiple versions (such as a version with GNOME and another with KDE), but that will require you to be more knowledgeable in building containers. Modification is more involved and if you want to leverage the images already built at `ublue-os/main` or `ublue-os/nvidia` you might have to modify their `build.yml`.
If you do decide to use [`main`](https://github.com/ublue-os/main) the *Manual setup* steps above still apply.

### You need to read the documentation
- There's no way around this, we're terraforming a new planet, you'll save a ton of time by reading the documentation:
    - [Silverblue](https://docs.fedoraproject.org/en-US/fedora-silverblue/)
    - [Kinoite](https://docs.fedoraproject.org/en-US/fedora-kinoite/)
    - [CoreOS](https://docs.fedoraproject.org/en-US/fedora-coreos/)
    - [startingpoint](https://github.com/ublue-os/startingpoint)
- You and your users might be more used to traditional desktops
    - On immutable systems, most software development tools shouldn't be installed directly on your base system. They should be run separate from the host system in some way, like using [a toolbox](https://universal-blue.org/guide/toolbox/) or [Podman](https://podman.io/) directly.
    - Most documentation around "How do I install a webserver in Fedora" will not apply
    - It looks more like `podman run --name podman-nginx -p 8080:80 -d nginx`

### Set up the pipeline first

Don't try to add something complicated out of the box, start with something basic, make a small change. 
Then ensure that the builds are working, are signed properly, and you get used to making changes in your repository.
This will save you a ton of time, because you can do revisions faster long term instead of getting stuck on something unrelated, spending a ton of time fixing it, and then realizing that you still have to fix the rest of the pipe.

> Get the water flowing first!

### Resist the urge to add the entire universe 
 - Systems like this are designed for a _small, lean, mean, maintainable, and performant core_. Remember that updates to the _base image_ require a reboot, so ideally you want that surface area to be small - let Flatpak and other userspace tools handle the rest.
 - But also remember that these systems are atomic, you don't need to manually clean up an old decision, the user will just get a new pristine image (ideally every day), so if you need to add a bunch of packages to get the desired outcome then you can always trim it down later - just remember that you need to account for the user's data!

### Remember where you _can_ add files
When making an image you can't put things in `/usr/local` or `/var/` (which includes the home directory) or other common places to put custom things as a system administrator. In this context you are the distro now; write to system directories like `/usr/bin`.