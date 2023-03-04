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

!!! warning

    Ensure you are forking the repository and NOT choosing "Use this template". The project moves quickly and it's important for you to get updates!

1. Fork the [ublue-os/base](https://github.com/ublue-os/main) repo:
1. Ensure your [GitHub Actions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository) and [GitHub Packages](https://docs.github.com/en/packages) are set up and enabled
1. Change the [image name in the action](https://github.com/ublue-os/base/blob/aab8078cfdc7d2354e057a0ca4771d3a53d2df4c/.github/workflows/build.yml#L14) to match what you want to call your image
   - Changing it to `IMAGE_NAME: beagles` will name the final image: `ghcr.io/yourusername/beagles` - so you'll likely want that to be your cool name instead of `base`
1. Choose your own Adventure:
   - Edit [packages.json](https://github.com/ublue-os/main/blob/main/packages.json) 
     - Add the rpm's you'd like to be included in your image
     - Flatpaks are a work in progress but you'll be able to edit a file
1. Generate a keypair
   - Install the [cosign CLI tool](https://edu.chainguard.dev/open-source/sigstore/cosign/how-to-install-cosign/)
   - Run `cosign generate-key-pair`
   - In your repository settings, under Secrets and Variables -> Actions
     - Create a new secret, make sure that you don't put a password on the key as this will be used by an action:
     ![image](https://user-images.githubusercontent.com/1264109/216735595-0ecf1b66-b9ee-439e-87d7-c8cc43c2110a.png)
     - Call it `SIGNING_SECRET` and then paste the contents of `cosign.key` into the field and save it. Be careful to make sure it's the .key file and not the .pub file. It should look like this:  
     ![image](https://user-images.githubusercontent.com/1264109/216735690-2d19271f-cee2-45ac-a039-23e6a4c16b34.png)
     - Copy the `cosign.pub` key into the root of your repository, replacing the key you got from here.
     - Copy the instructions from the verification section of this readme and make adjustments to your container url. This part is important, users must have a method of verifying the image. The linux desktop must not lag behind in cloud when it comes to supply chain security, so we're starting right from the start! (Seriously don't skip this part) 
1. Start making modifications to your Containerfile!
   - Change a few things and keep an eye on your Actions and Packages section of your repo, you'll generate a new image one every merge and additionally every day. 
   - Follow the instructions at the top of this repo but this time with the `ghcr.io/yourusername/beagles` url and then you'll be good to go!
   - Hang out in the [discussions forums](https://github.com/orgs/ublue-os/discussions) with others to share tips and get help, enjoy!

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
