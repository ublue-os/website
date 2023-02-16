---
hide:
  - navigation
---

## Custom Operating System images based on Fedora

This is a collection of container images using Fedora's support for OCI/Docker containers as a [transport and delivery mechanism for operating system content](https://fedoraproject.org/wiki/Changes/OstreeNativeContainerStable). That's nerdspeak for the ultimate Linux client: the reliability of a Chromebook, but with the flexibility and power of a traditional Linux desktop. At long last, we've ascended. 

This project's purpose is to:

- Provide a diverse set of Fedora based images for people to use as their desktop operating system.
- Provide a diverse set of tools and reusable automation "kits" for more technical users so that they can customize and share their images with others.
- Act as a proving ground for new ideas around the Linux desktop. 

!!! example "Join us on the journey"

    [Full list of images](https://ublue.it/images)

Our images offer GNOME, KDE, XFXE, LXQt, and MATE, with more being added on the regular. Our NVIDIA images offer a unique blend of reliability and ease of use that you won't find anywhere else.

## Why would I use these?

These images reflect a more [cloud-native](https://www.youtube.com/watch?v=vZ1LRe_foJY) approach to running Linux on your desktop. 

### Advantages over traditional Linux desktops 

- Reliable, atomic updates with built in rollback
- Known-good state and fewer failures
    - Significantly reduced configuration drift
    - No compiling or building Nvidia drivers on the local client, they come premade on the image
- Clean seperation of the base system from applications and your data
- Unbridled customization
    - Craft your perfect image from scratch or derive from others   
- Reuses standards-based tooling from cloud
    - Built using ostree-enabled [OCI compliant images](https://opencontainers.org/) 
- Built-in container tools for developers
    - Consume packages and software from any repo without risking breakage on the client
- Reuses standards-based tooling from cloud
    - Built using ostree-enabled [OCI compliant images](https://opencontainers.org/)
    - Host and Build on any container registry, both cloud and bare metal
- Built-in container tools for developers

### Other Features

- Fast updates: minimum of once-a-day updates so you're never behind Fedora
- Hosted on ghcr.io
    - Ninety (90) days of image archives allowing for flexible rollback options  
    - Globally distributed via CDN for fast image downloads, thanks Microsoft!
- Images signed with standard [sigstore tools](https://www.sigstore.dev/)

## Join Us

We're always looking for people to help, all skill levels and areas of expertise are welcome.

- [Join our Discord](https://discord.gg/WEu6BdFEtp)
- Pull requests wanted and accepted!
- Experimentation encouraged!

If you're building your own custom images feel free to add them to [our awesome list](https://github.com/ublue-os/awesome-custom-images)!
