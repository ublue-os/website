# Purpose

This project generates [operating system images](images.md) that you can use on your own PC.
However, one of the main goals is to provide a custom toolkit for you to make your own custom image. 

!!! Note "This is moving fast"

    It's still early in the project's life, we're in need of people to help with these docs, so if you find a problem please consider [submitting a pull request](https://github.com/ublue-os/website) to help us improve.

## Why make your own image?

The concept around image based operating systems balances on the idea that the core image is ready to go, ideally users don't need to touch it.
However, people like to tinker, so instead of [layering packages](https://docs.fedoraproject.org/en-US/iot/adding-layered/) that compromise the integrity of upgrades, the idea is to just make your own image so that you can just have a pristine setup over time for the life of the hardware.

### Reasons to make your own image
- You want the reliability of image based operating systems like ChromeOS or Android but want more flexibility
    - A complete Fedora experience with all the benefits of your preferences shipped out of the box
    - Ship your own terminal CLI experience on whatever distribution you like
- Draw "outside the lines" of what Fedora provides in a repeatable manner
    - Make your own custom image without the overhead or responsibility of "making your own distro"
    - But still be able to ingest all the improvements from Fedora every day
- You might need a specific kernel or module to get your hardware to work
- It's fun

# Making your Own

## Should I use [`ublue-os/main`](https://github.com/ublue-os/main) or [`ublue-os/startingpoint`](https://github.com/ublue-os/startingpoint)?

The instructions below recommend `startingpoint` because it is:  

- Intended for modification and to be a simple template
- More suitable for personal usage
- Has an easier to edit configuration format, YAML, which also supports comments and inline documentation

Making a custom image using `main` instead would be better if you intend on having multiple versions (such as a version with GNOME and another with KDE), but modification is more involved and if you want to leverage the images already built at `ublue-os/main` or `ublue-os/nvidia` you have to modify the `build.yml`.  
If you do decide to use `main` the *Manual setup* steps below still apply.

## Automatic setup 

You can quickly set up a GitHub repository that builds a functional native container image based on [ublue-os/startingpoint](https://github.com/ublue-os/startingpoint) using the (experimental) community-maintained [`create-ublue-image`-tool](https://github.com/EinoHR/create-ublue-image).

1. Ensure you have [Podman](https://podman.io/) installed. If you're already using Fedora Silverblue, you should already have it.
2. Run the command `podman run -v "$(pwd)":/host:z -it ghcr.io/einohr/create-ublue-image`
    - This will mount the current directory for modification inside the container. If you want the folder containing your repo to be in a certain directory like `~/dev`, you should `cd` into that before executing the tool.
3. Follow the instructions the tool gives you

In order to update changes from the upstream repository, run:
```
git fetch upstream
git merge upstream/main -m "chore: merging upstream changes"
```

## Manual setup

!!! warning

    Ensure you are forking the repository and NOT choosing "Use this template". The project moves quickly and it's important for you to get updates!

### Create and configure your repository

1. Fork the [ublue-os/startingpoint](https://github.com/ublue-os/startingpoint) repo:
1. Change the image name in [the action](https://github.com/ublue-os/startingpoint/blob/main/.github/workflows/build.yml) (you can just replace "startingpoint" with the name of your choice) to match what you want to call your image
    - Changing it to `beagles` will name the final image: `ghcr.io/yourusername/beagles` - you'll likely want that to be your cool name instead of `base`
1. Ensure your [GitHub Actions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository) and [GitHub Packages](https://docs.github.com/en/packages) are set up and enabled
1. [Optional] Install the [Semantic PRs](https://github.com/marketplace/semantic-prs) GitHub app if you want nice changelogs

### Set up container signing

Container signing is important for end-user security and is enabled on all uBlue images. It is highly recommended you set this up, and by default the image builds *will fail* if you don't.

This part is important, users must have a method of verifying the image. The Linux desktop must not lag behind in cloud when it comes to supply chain security, so we're starting right from the start! (Seriously don't skip this part) 

!!! warning

    Be careful to *never* accidentally commit `cosign.key` into your git repo.

1. Generate a key pair
    1. Install the [cosign CLI tool](https://edu.chainguard.dev/open-source/sigstore/cosign/how-to-install-cosign/)
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

1. Edit `recipe.yml` to modify your image
    - You can configure what packages to install, what to name the image, with more information inside the file
1. Edit the `Containerfile` for more in-depth changes such as adding configuration files
    - For example, if you have a folder called `etc` inside your repository, you can add it to the image by adding `COPY etc /etc` to the `Containerfile`. Then you can add any system configuration files inside `etc`, and they will be shipped with your image.
    - Files cannot be added under `/var`
1. After you've changed a few things and keep an eye on your Actions and Packages section of your repo, you'll generate a new image on every merge and additionally every day. 
1. Hang out in the [discussions forums](https://github.com/orgs/ublue-os/discussions) with others to share tips and get help, enjoy!

# Best Practices

The following are some best practices based on experience with learning how to move to this new model:

### You need to read the documentation
- There's no way around this, we're terraforming a new planet, you'll save a ton of time by reading the documentation:
    - [CoreOS](https://docs.fedoraproject.org/en-US/fedora-coreos/)
    - [Kinoite](https://docs.fedoraproject.org/en-US/fedora-kinoite/)
    - [Silverblue](https://docs.fedoraproject.org/en-US/fedora-kinoite/)
- Additionally, your developer users might not be familiar with [Podman](https://podman.io/)
    - Most documentation around "How do I install a webserver in Fedora" will not apply
    - It looks more like `podman run --name podman-nginx -p 8080:80 -d nginx`
    - IDEs are still a problem area 

### Resist the urge to add the entire universe 
 - Systems like this are designed for a _small, lean, mean, maintainable, and performant core_. Remember that updates to the _base image_ require a reboot, so ideally you want that surface area to be small - let Flatpak handle the rest.
 - But also remember that these systems are atomic, you don't need to manually clean up an old decision, the user will just get a new pristine image (ideally every day), so if you need to add a bunch of packages to get the desired outcome then you can always trim it down later - just remember that you need to account for the user's data!
 - This means: be cognizant where you put stuff. When making an image you can't put things in `/usr/local` or other common places to put custom things, in this context you're the distro now: so probably `/usr/bin`. Don't worry, you got this.
