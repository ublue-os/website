---
hide:
  - navigation
---

This list is in alphabetical order, organized by build method.
Check out [artifact hub](https://artifacthub.io/packages/search?org=ublue-os&sort=relevance&page=1) for more images that we may be publishing.

- **Users:** the build method doesn't matter to you, use whichever image fits your use case.
- **Creators:** The method that the image is built might be important to you

!!! warning

    If you're coming from an existing Fedora installation you should ensure that you don't have layered packages. If you're not familiar with usage of rpm-ostree we strongly recommend [reading the documentation](https://coreos.github.io/rpm-ostree/).

## Composed Images

These images are built by composing ostree treefiles and are more "from scratch".
Use this method if you want to build your image from scratch with ostree. 

| Image name | Description | Status | 
| ---------- | ----------- | ------ | 
| [`lxqt`](https://github.com/ublue-os/lxqt) | Immutable Fedora-based LXQt desktop container image  | [![lxqt](https://github.com/ublue-os/lxqt/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/lxqt/actions/workflows/build.yml) |
| [`mate`](https://github.com/ublue-os/mate) | Immutable Fedora-based MATE Desktop container image | [![mate](https://github.com/ublue-os/mate/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/mate/actions/workflows/build.yml) |
| [`vauxite`](https://github.com/ublue-os/vauxite) | Immutable Fedora-based Xfce desktop | [![vauxite](https://github.com/ublue-os/vauxite/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/vauxite/actions/workflows/build.yml) |

## Common Images

These images are composed from Fedora's published images.
They do NOT include Nvidia drivers, but do include codecs and other convenience features.
They can be used as desktops or as an image to derive from.

- [Check them out on GitHub](https://github.com/ublue-os/main) for instructions and to learn more!

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/bazzite/bazzite" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>bazzite</b>: Bazzite is intended to be an alternative OS for the Steam Deck</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/bazzite/bazzite">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/kinoite-main/kinoite-main" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>silverblue-main</b>: A Kinoite (KDE) image with batteries included</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/kinoite-main/kinoite-main">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/silverblue-main/silverblue-main" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>silverblue-main</b>: A Silverblue (GNOME) image with batteries included</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/silverblue-main/silverblue-main">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/sericea-main/sericea-main" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>sericea-main</b>: A Sericea (Sway) image with batteries included</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/sericea-main/sericea-main">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/ubuntu/ubuntu" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>ubuntu</b>: Fedora Silverblue for Ubuntu Expatriates</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/ubuntu/ubuntu">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

## Images with Nvidia Drivers

These include all the quality-of-life features of the main images plus Nvidia drivers. 

- [Check them out on GitHub](https://github.com/ublue-os/nvidia) for instructions and to learn more!

## Base Images for Alternate Desktops

These images are a starting point, just add your own desktop or window manager:

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/base-main/base-main" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>base-main</b>: A base base-main image with batteries included</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/base-main/base-main">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>
