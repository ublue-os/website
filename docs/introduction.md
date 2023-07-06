# Introduction to image-based Linux distributions from Fedora and Universal Blue

Image-based in the context of Linux distributions means that the operating system is packaged as a sort of image and everything added by the user is considered a separate layer. In image-based distributions the root filesystem is mounted as read-only while the OS is booted. This means that all the changes to the base system are only applied after a reboot. Fedora uses [`ostree`](https://ostreedev.github.io/ostree/) (like git for the filesystem) for its atomic filesystem updates and [`rpm-ostree`](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/rpm-ostree/) (specialized equivalent of Fedora's `dnf`) for the image and package management system.

## Isn't this just another immutable Linux distribution?

Fedora Silverblue, Kinoite, Sericea, etc. are all called immutable. So is VanillaOS.   
We think that it is a misleading term with the connotation of the end user losing their power.
TODO: figure out this section

## What does uBlue do?

Universal Blue uses ["OSTree Native Containers"](https://fedoraproject.org/wiki/Changes/OstreeNativeContainerStable) which enables "rebasing" (changing out the base system while keeping user data) the operating system to an [OCI](https://opencontainers.org/) container image (same thing as Docker container images).  
The Universal Blue project builds *light-touch* images of the image-based Fedora variants with QoL additions that don't diverge too much from the base of Fedora. [Read more about our goals on the Scope page.](https://universal-blue.org/scope/)  
Additionally, the uBlue project works on more opinionated images such as [Bluefin](https://github.com/ublue-os/bluefin) and [Bazzite](https://github.com/ublue-os/bazzite), and develops related utilities such as [yafti](https://github.com/ublue-os/yafti) for firstboot setup and [fleek](https://github.com/ublue-os/fleek) for managing your home directory with [Nix](https://nixos.org/) in an easier way.  
We also provide tools for the average Linux nerd to build their own image using our templates and processess, which can be used to ship some light configuration to all of your machines, or finally make the Linux distribution you've long wished for but never had the tools to create. [Read more about creating your own image here.](http://universal-blue.org/tinker/0-make-your-own/)

## Cloud-native

All of Universal Blue rests on the idea of [cloud-native](https://en.wikipedia.org/wiki/Cloud-native_computing). We leverage standard cloud tools like the OCI standard and the GitHub Container Registry to build our images. This is a much lighter and faster way of building and deploying Linux environments to users that allows professionals in the industry to leverage their pre-existing knowledge to create a better desktop Linux experience.

## Mindset

Best practices when using an image-based Linux distribution differ from the usual ways of managing your system in more traditional Linux environments. For example, when installing software you shouldn't always reach for the system package manager, `rpm-ostree` in this case. When keeping the amount of packages layered on top of the base image to a minimal, system updates will be quicker and are more likely to succeed, for example. [Read more about other ways of installing software here.](https://universal-blue.org/guide/software/)

Most documentation around "how do I do XYZ in Fedora/Linux" will not apply. Instead, you can do things such as running a webserver with [`podman`](https://podman.io/) and containers. And for setting up development or installing software not available as Flatpaks you should use some encapsulated userspace environment such as a [toolbox](https://universal-blue.org/guide/toolbox/) or [devbox](https://www.jetpack.io/devbox/).

You should familiarize yourself with the documentation of Universal Blue and related projects:

- [Silverblue](https://docs.fedoraproject.org/en-US/fedora-silverblue/)
- [Kinoite](https://docs.fedoraproject.org/en-US/fedora-kinoite/)
- [CoreOS](https://docs.fedoraproject.org/en-US/fedora-coreos/)
- [IoT](https://docs.fedoraproject.org/en-US/iot/)
- [rpm-ostree](https://coreos.github.io/rpm-ostree/)

You can always ask for help from our [Community](https://universal-blue.org/CODE_OF_CONDUCT/) (see sidebar).

## Read-only and writable directories

Image-based Fedora variants follow the [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) while mounting some directories as read-only and symlinking some from their actual location to their FHS-compatible location.

`/usr/` is read-only when booted while `/var/` and `/etc/` are writable. Everything in `/var/` is locally managed and cannot be directly changed by images. Certain directories in the root directory are symlinked to either `/usr/` or `/var/`, for example, `/home/` is symlinked to `/var/home/`. `/usr/local/` is writable and files can be added, and system configuration modified there. 