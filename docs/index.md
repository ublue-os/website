---
hide:
  - navigation
---

## Custom Operating System images based on Fedora

This is a collection of container images using Fedora's support for OCI/Docker containers as a [transport and delivery mechanism for operating system content](https://fedoraproject.org/wiki/Changes/OstreeNativeContainerStable). That's nerdspeak for the ultimate Linux client: the reliability of a Chromebook, but with the flexibility and power of a traditional Linux desktop. At long last, we've ascended. 

This project's purpose is to:

<div class="grid cards" markdown> 

- :fontawesome-container-storage: { .lg .middle } __Images__
  --- 
  Provide a diverse set of [continuously delivered](https://en.wikipedia.org/wiki/Continuous_delivery) Fedora-based images for people to use as their desktop operating system
  
- :fontawesome-screwdriver-wrench: { .lg .middle } __Toolkit__
  ---
  Provide a diverse set of tools and [a reusable automation kit](https://github.com/ublue-os/startingpoint) for more technical users so that they can customize and share their images with others
  
- :fontawesome-explosion: { .lg .middle } __Experimentation__
  ---
  Act as a proving ground for new ideas around the Linux desktop like [Fleek](https://getfleek.dev/), [Yafti](https://github.com/ublue-os/yafti), and [Boxkit](https://github.com/ublue-os/boxkit)
  
- :fontawesome-heart: { .lg .middle } __Contributions__
  ---
  Help new contributors to start their cloud native and open source journeys no matter their skill level

</div> 
  
Our images offer GNOME, KDE, XFCE, LXQt, and MATE, with more being added on the regular. Our NVIDIA images offer a unique blend of reliability and ease of use that you won't find anywhere else.

## Why would I use these?

These images reflect a more [cloud-native](https://en.wikipedia.org/wiki/Cloud-native_computing) approach to running Linux on your desktop. We feel that a dedicated group of enthusiasts can automate a large amount of toil that plagues existing Linux desktops today. This is achieved by reusing cloud technologies as a delivery mechanism to deliver a more reliable experience. 

![type:video](https://www.youtube.com/embed/vZ1LRe_foJY)

## Usage

[Download the ISO :fontawesome-solid-heart:](https://github.com/ublue-os/main/releases){ .md-button .md-button--primary }

One small ISO with options to install GNOME, KDE, XFCE, LXQt, and MATE, as well as Nvidia-integrated versions of each. 
    
!!! example "... and then follow this!"

    [Installation Instructions](/installation)

You can always rebase from one image to another, don't worry, that operation is image-based, so you'll always have what's supposed to be there 

Image based updates inherently don't allow for cruft to accumulate, allowing for a level of stability and upgrade resilience that has been missing on the Linux desktop, until now. 
Our goal is to for one install to last the life of the hardware.

### Advantages over traditional Linux desktops 

- Reliable, atomic updates with built in rollback
- Known-good state and fewer failures
    - Significantly reduced configuration drift
    - No compiling or building Nvidia drivers on the local client, they come premade on the image
- Clean seperation of the base system from applications and your data
    - Integration of Flatpak applications via [Flathub](https://flathub.org/home)
    - [Toolbox](https://github.com/containers/toolbox) and [Distrobox](https://github.com/89luca89/distrobox) support, run applications from any distribution in a containerized environment 
- Unbridled customization
    - Craft your perfect image from scratch or derive from others   
- Reuses standards-based tooling from cloud
    - Built using ostree-enabled [OCI compliant images](https://opencontainers.org/) 
- Built-in container tools for developers
    - Consume packages and software from any repo without risking breakage on the client
    - Easy consumption of other OCI images, if it's on the [CNCF Landscape](https://landscape.cncf.io/) it's a first class citizen thanks to Podman!

!!! example "What we mean by reliability"

    An important concept with this model is that the system is designed to reliably deliver your software. That means that if you were destined to get a kernel bug that day ... well, at least the package got to you in way better condition than your last carrier. At least you have a safe rollback. This might sound counterintuitive at first, but be level of efficiency improves so dramatically over the long term that allows it developers to catch issues like that earlier in the testing process. 

### Other Features

- Rebase back to pure [Fedora](https://getfedora.org/en/) without reinstallation
- Fast updates: minimum of once-a-day updates so you're never behind Fedora
- Hosted on ghcr.io
    - Ninety (90) days of image archives allowing for flexible rollback options  
    - Globally distributed via CDN for fast image downloads, thanks Microsoft!
- Images signed with standard [sigstore tools](https://www.sigstore.dev/)
- And some more features explained here:

![type:video](https://www.youtube.com/embed/X8h304Jp9N8?start=435)

## Join Us

We're always looking for people to help, all skill levels and areas of expertise are welcome. Check out [the roadmap](https://github.com/orgs/ublue-os/projects/1) and [proposals](https://github.com/orgs/ublue-os/discussions?discussions_q=is%3Aopen+label%3Aproposal) to get a feel for the project, then: 

- [Join our Discord](https://discord.gg/WEu6BdFEtp)
  - We strive for a safe, inclusive community   
- Pull requests encouraged and accepted

If you're building your own custom images feel free to add them to [our awesome list](https://github.com/ublue-os/awesome-custom-images)!
