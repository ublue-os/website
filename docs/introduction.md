# Introduction to image-based Linux distributions from Fedora and Universal Blue

"Image-based," in the context of Linux distributions, means that the operating system is packaged as an image and everything added by the user is considered a separate layer. In image-based distributions, the root filesystem is mounted as read-only while the OS is booted. This means that all the changes to the base system are only applied after a reboot. Fedora uses [`ostree`](https://ostreedev.github.io/ostree/) (like `git` for the filesystem) for its atomic filesystem updates and [`rpm-ostree`](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/rpm-ostree/) (specialized equivalent of Fedora's `dnf`) for the image and package management system.

## What does Universal Blue do?

Universal Blue uses the ["OSTree Native Containers"](https://fedoraproject.org/wiki/Changes/OstreeNativeContainerStable) feature of Fedora which enables using [OCI](https://opencontainers.org/) container images to distribute the operating system.

The Universal Blue project builds *light-touch* images of the image-based Fedora variants with quality-of-life additions that don't diverge too much from the base of Fedora. [Read more about our goals on the Scope page.](https://universal-blue.org/scope/).
Additionally, the project works on more opinionated images such as [Bluefin](https://github.com/ublue-os/bluefin) and [Bazzite](https://github.com/ublue-os/bazzite), and develops related utilities such as [yafti](https://github.com/ublue-os/yafti) for first-boot setup and [fleek](https://github.com/ublue-os/fleek) for managing your home directory with [Nix](https://nixos.org/).

We also provide tools for users to build their own image using our templates and processes, which can be used to ship some light configuration to all of your machines, or finally make the Linux distribution you've long wished for, but never had the tools to create. [Read more about creating your own image here.](http://universal-blue.org/tinker/make-your-own/).

## Cloud-native

All of Universal Blue rests on the idea of [cloud-native](https://en.wikipedia.org/wiki/Cloud-native_computing). We leverage standard cloud tools like the [OCI standard](https://opencontainers.org/) and the GitHub Container Registry to build our images. This is a much lighter and faster way of building and deploying Linux environments to users that allows professionals in the industry to leverage their pre-existing knowledge to create a better desktop Linux experience.

## Mindset

Best practices when using an image-based Linux distribution differ from more traditional Linux environments. For example, installing software is typically done in a container or a different method rather than using the system package manager. Read more about other ways of installing software [here](https://universal-blue.org/guide/software/).

Most documentation around "how do I do XYZ in Fedora/Linux" will not apply. Instead, you can do things such as running a web-server with [`podman`](https://podman.io/) and containers. And for setting up development or installing software not available as Flatpaks you should use some encapsulated user-space environment such as a [toolbox](https://universal-blue.org/guide/toolbox/) or [devbox](https://www.jetpack.io/devbox/).

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
