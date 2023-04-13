---
hide:
  - navigation
---

## Custom Operating System images based on Fedora

This is a collection of container images using Fedora's support for OCI/Docker containers as a [transport and delivery mechanism for operating system content](https://fedoraproject.org/wiki/Changes/OstreeNativeContainerStable). That's nerdspeak for the ultimate Linux client: the reliability of a Chromebook, but with the flexibility and power of a traditional Linux desktop. At long last, we've ascended. 

This project's purpose is to:

- Provide a diverse set of [continuously delivered](https://en.wikipedia.org/wiki/Continuous_delivery) Fedora-based images for people to use as their desktop operating system
- Provide a diverse set of tools and reusable automation "kits" for more technical users so that they can customize and share their images with others
- Act as a proving ground for new ideas around the Linux desktop
- Help new contributors to start their cloud native and open source journeys no matter their skill level

Our images offer GNOME, KDE, XFCE, LXQt, and MATE, with more being added on the regular. Our NVIDIA images offer a unique blend of reliability and ease of use that you won't find anywhere else.

## Why would I use these?

These images reflect a more [cloud-native](https://en.wikipedia.org/wiki/Cloud-native_computing) approach to running Linux on your desktop. We feel that a dedicated group of enthusiasts can automate a large amount of toil that plagues existing Linux desktops today.

![type:video](https://www.youtube.com/embed/vZ1LRe_foJY)

## Usage

!!! example "Try it today!"

    [Installation Media](https://github.com/ublue-os/main/releases) - netinstall installation
    
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

We're always looking for people to help, all skill levels and areas of expertise are welcome.

- [Join our Discord](https://discord.gg/WEu6BdFEtp)
  - We strive for a safe, inclusive community   
- Pull requests wanted and accepted
- Experimentation encouraged

If you're building your own custom images feel free to add them to [our awesome list](https://github.com/ublue-os/awesome-custom-images)!
