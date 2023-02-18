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
Use this method if you want to build your image from scratch. 

| Image name | Description | Status | 
| ---------- | ----------- | ------ | 
| [`lxqt`](https://github.com/ublue-os/lxqt) | Immutable Fedora-based LXQt desktop container image  | [![lxqt](https://github.com/ublue-os/lxqt/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/lxqt/actions/workflows/build.yml) |
| [`mate`](https://github.com/ublue-os/mate) | Immutable Fedora-based MATE Desktop container image | [![mate](https://github.com/ublue-os/mate/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/mate/actions/workflows/build.yml) |
| [`vauxite`](https://github.com/ublue-os/vauxite) | Immutable Fedora-based Xfce desktop | [![vauxite](https://github.com/ublue-os/vauxite/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/vauxite/actions/workflows/build.yml) |

## Container-derived Images

These images are composed from Fedora's published images.
Use this method if you want to just make changes to a published image:

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/ublue/base" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>base</b>: Modified Fedora Silverblue with unfiltered Flathub, distrobox, and automatic updates</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/ublue/base">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/base-nvidia/base-nvidia" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>nvidia</b>: Vanilla Fedora Silverblue with Nvidia drivers added</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/base-nvidia/base-nvidia">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/bazzite/bazzite" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>bazzite</b>: Bazzite is based off of ublue-os/kinoite-nvidia that is intended to be an alternative OS for the Steam Deck</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/bazzite/bazzite">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/bazzite-desktop/bazzite-desktop" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>bazzite-desktop</b>: Bazzite-desktop is based off of ublue-os/kinoite-nvidia and is intended to be a SteamOS-alike for desktops. </p>&mdash; Open in <a href="https://artifacthub.io/packages/container/bazzite-desktop/bazzite-desktop">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/nvidia/kinoite-nvidia" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>nvidia</b>: Vanilla Fedora Kinoite with Nvidia drivers added</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/nvidia/kinoite-nvidia">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/silverblue-nvidia/silverblue-nvidia" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>nvidia</b>: Vanilla Fedora Silverblue with Nvidia drivers added</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/silverblue-nvidia/silverblue-nvidia">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/ubuntu/ubuntu" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>ubuntu</b>: Fedora Silverblue for Ubuntu Expatriates</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/ubuntu/ubuntu">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>

<div class="artifacthub-widget" data-url="https://artifacthub.io/packages/container/vauxite-nvidia/vauxite-nvidia" data-theme="light" data-header="false" data-stars="true" data-responsive="true"><blockquote><p lang="en" dir="ltr"><b>vauxite-nvidia</b>: Vanilla Vauxite with Nvidia drivers added</p>&mdash; Open in <a href="https://artifacthub.io/packages/container/vauxite-nvidia/vauxite-nvidia">Artifact Hub</a></blockquote></div><script async src="https://artifacthub.io/artifacthub-widget.js"></script>
