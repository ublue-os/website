---
hide:
  - navigation
---

# Custom Operating System images based on Fedora

This is a collection of container images using Fedora's support for OCI/Docker containers as a [transport and delivery mechanism for operating system content](https://fedoraproject.org/wiki/Changes/OstreeNativeContainerStable). That's nerdspeak for the ultimate Linux client: the reliability of a Chromebook, but with the flexibility and power of a traditional Linux desktop. At long last, we've ascended.

For a more in-depth explanation, refer to our [Documentation,](/introduction) and [Media Coverage](/media) sections.

This project provides ... 

<div class="grid cards" markdown>

- :material-train-car-container:{ .lg .middle } __Images__

    ---
    A diverse set of [continuously delivered](https://en.wikipedia.org/wiki/Continuous_delivery) Fedora-based images for people to use as their desktop operating system

- :material-toolbox:{ .lg .middle } __Toolkit__

    ---
    A diverse set of tools and [a reusable automation kit](https://github.com/ublue-os/startingpoint) for more technical users so that they can customize and share their images with others

- :material-speedometer:{ .lg .middle } __Experimental Applications__

    ---
    Act as a proving ground for new ideas around the Linux desktop like [Fleek](https://getfleek.dev/), [Forge](https://github.com/ublue-os/forge), [Yafti](https://github.com/ublue-os/yafti), and [Boxkit](https://github.com/ublue-os/boxkit)

- :material-heart:{ .lg .middle } __Community__

    ---
    Help new contributors to start their cloud native and open source journeys no matter their skill level.

</div>
  
Our images offer GNOME, KDE, XFCE, LXQt, Budgie, and MATE, with more being [added regularly](/images). Our [NVIDIA images](/images/nvidia) offer a unique blend of reliability and ease of use that you won't find anywhere else. These are offered in a variety of images to fit your needs:

- [Asus](/images/asus) - Fedora-based images with [asus-linux.org](https://asus-linux.org) kernels
- [Framework](/images/framework) - Framework's recommended Fedora settings 
- [Legion](/images/legion) - Fedora-based images with support Lenovo Legion laptops and Legion Go
- [Surface](/images/surface) - Fedora-based images with [linux-surface](https://github.com/linux-surface/linux-surface) kernels

Check out [Bazzite](/images/bazzite), the ultimate gaming setup for your PC, Steam Deck, ASUS ROG Ally and Legion Go. Fedora's upstream pipeline automated directly to your device, nice. 

[Bluefin](/images/bluefin) is a simple to use desktop with the mission of serving a mass audience. The [Bluefin DX](/images/bluefin/developer-experience) edition is designed to be the ultimate Linux workstation for open source developers.

And last, but not least, check out [Beyond](https://github.com/ublue-os/beyond), our collaboration with [Cassidy James Blaede](https://cassidyjames.com/), a peek into his vision of a future GNOME desktop. 

## Why would I use these?

These images reflect a more [cloud-native](https://en.wikipedia.org/wiki/Cloud-native_computing) approach to running Linux on your desktop. We feel that a dedicated group of enthusiasts can automate a large amount of toil that plagues existing Linux desktops today. This is achieved by reusing cloud technologies as a delivery mechanism to deliver a more reliable experience. To quote the [goals of bootc](https://github.com/containers/bootc):

> A toplevel goal is that every tool and technique a Linux system administrator knows around how to build, inspect, mirror and manage application containers also applies to bootable host systems.

We like the sound of that, and we're hoping to be your "Desktop DevOps team". Bringing the patterns from the server world to the desktop world means that there is a new layer on top of the distribution. You can now atomically share maintenance of things that people currently do by hand as post-installation. Universal Blue automates that. Contributors use a [gitops approach](https://github.com/open-gitops/documents/blob/main/PRINCIPLES.md) to maintaining these images, all out in the open for everyone to inspect, resulting in a system that now leverages the expertise of system administrators right to your desktop. It's pretty awesome. 

If you want to learn, come hang out. We are here to teach and learn from each other!

<iframe width="560" height="315" src="https://www.youtube.com/embed/vZ1LRe_foJY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>  

## Usage

[Download the ISO :fontawesome-solid-heart:](https://github.com/ublue-os/main/releases){ .md-button .md-button--primary }

One small ISO with options to install GNOME, KDE, XFCE, LXQt, and MATE, as well as Nvidia-integrated versions of each.

!!! example "... and then follow this!"

    [Installation Instructions](/installation)

You can always rebase from one image to another, don't worry, that operation is image-based, so you'll always have what's supposed to be there.

Image based updates inherently don't allow for cruft to accumulate, allowing for a level of stability and upgrade resilience that has been missing on the Linux desktop, until now...

Our goal is to for one install to last the life of the hardware.

### Advantages over traditional Linux desktops

- Reliable, atomic updates with built in rollback
- Known-good state and fewer failures:
    - Significantly reduced configuration drift
    - No compiling or building Nvidia drivers on the local client, they come pre-made on the image
    - [Kernel mods](https://github.com/ublue-os/akmods) right on the image 
- Clean separation of the base system from applications and your data
    - Integration of Flatpak applications via [Flathub](https://flathub.org/home).
    - [Toolbox](https://github.com/containers/toolbox) and [Distrobox](https://github.com/89luca89/distrobox) support, run applications from any distribution in a containerized environment
- Unbridled customization:
    - Craft your perfect image from scratch or derive from others
- Community Maintained
    - The project is maintained by a community of cloud-native contributors with an [explicit mission](/mission)
- Reuses standards-based tooling from cloud:
    - Built using ostree-enabled [OCI compliant images](https://opencontainers.org/)
- Built-in container tools for developers:
    - Consume packages and software from any repo without risking breakage on the client
    - Easy consumption of other OCI images, if it's on the [CNCF Landscape](https://landscape.cncf.io/) it's a first class citizen thanks to Podman!

!!! example "What we mean by reliability:"

    An important concept with this model is that the system is designed to reliably deliver your software. Software bugs and issues still occur with individual software. We mean reliability when it comes to installation and upgrades of the entire system, if you were destined to get a kernel bug that day, it still happens. This might sound counterintuitive at first, but be level of efficiency improves so dramatically over the long term that it allows developers to catch issues earlier in the testing process. This is awesome stuff, ask your local cloud nerd.  

### Other Features

- Rebase back to pure [Fedora](https://getfedora.org/en/) without reinstallation. This is why we don't call it a distribution, it's an atomic layer of customization on an existing distribution that can be removed. 
- Fast updates: minimum of once-a-day updates so you're never behind Fedora.
- Hosted on ghcr.io:
    - Ninety (90) days of image archives allowing for flexible rollback options.
    - Globally distributed via CDN for fast image downloads, thanks Microsoft!
- Images signed with standard [sigstore tools](https://www.sigstore.dev/).
- And some more features explained here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/X8h304Jp9N8?start=435" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>  

## Join Us

We're always looking for people to help, all skill levels and areas of expertise are welcome. Check out [the roadmap](https://github.com/orgs/ublue-os/projects/1) to get a feel for the project, then: 

- Discuss the project with us on [Discourse](https://universal-blue.discourse.group/).
- [Join our Discord](https://discord.gg/WEu6BdFEtp)
  - We strive for a safe, inclusive community.
- Pull requests encouraged and accepted.

If you're building your own custom images feel free to add them to [our awesome list](https://github.com/ublue-os/awesome-custom-images)!
