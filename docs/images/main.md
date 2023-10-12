# Main

[![build-ublue](https://github.com/ublue-os/main/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/main/actions/workflows/build.yml)

A common main image for all other uBlue images, with minimal (but important) adjustments to Fedora. 💙

1. [Features](#Features)
2. [Tips and Tricks](#Tips-and-Tricks)
3. [How to Install](#How-to-Install)
4. [Verification](#Verification)
5. [Configuring Automatic Updates](/faq/#how-do-i-configure-automatic-updates)
6. [Making your own](https://universal-blue.org/tinker/make-your-own/)

## What is this?

For context, please familiarize yourself with [image-based desktops](https://silverblue.fedoraproject.org/about). These are Fedora OStree images that have been modified with the following quality of life features:

## Features

- Starts with a Fedora image,
- Adds the following packages to the base image:
  - Hardware acceleration and codecs,
  - `distrobox` for terminal CLI and user package installation
  - A selection of [udev rules and service units](https://github.com/ublue-os/config),
  - [libratbag](https://github.com/libratbag/libratbag), to configure supported mice via [piper](https://github.com/libratbag/piper),
  - Various other tools: check out the [complete list of packages](https://github.com/ublue-os/main/blob/main/packages.json).
- Sets automatic staging of updates for the system.
- Sets `flatpaks` to update twice a day.
- Everything else (desktop, artwork, etc) remains stock so you can use this as a good starting image.


!!!Note
    Universal Blue `*-main` images ***previously included*** a selection of pre-built kernel drivers (kmods) (`xpadneo, xpad-noone, xone, openrazer, v4l2loopback, wl`).
    Starting with the Fedora 39 release, [these are no longer included](https://github.com/ublue-os/main/issues/369) as they proved too opinionated, causing issues for downstream image builders using alternative kernels, etc.

    Downstream images are still encouraged to include these drivers in their builds.  See [Universal Blue akmods](https://github.com/ublue-os/akmods).

## Tips and Tricks

Unlike traditional Linux distributions, the base image is intended to be used "out-of-the-box" as it is. Packages are installed via Flatpak whenever possible (except for IDEs in some cases, more below).
Should that not be possible, you can use [distrobox](https://github.com/89luca89/distrobox) to have images of mutable distributions where you can install applications normally.

Want an application that is only available on Arch Linux *and* one that is only on Ubuntu? Well, now can have both!

Distrobox is very powerful; for example, you can use it to [host your entire development environment](https://github.com/89luca89/distrobox/blob/main/docs/posts/integrate_vscode_distrobox.md) completely separate from your host system. Or use it to run a [container for your virtual machines](https://github.com/89luca89/distrobox/blob/main/docs/posts/run_libvirt_in_distrobox.md).

`ublue-os/base-main` is also very well suited for servers, and users are expected to make full use of `podman` to host containers running "typical" server software i.e. `nginx`, `caddy` and others.

## How to Install

[Follow these instructions](/installation).

[File an issue](https://github.com/ublue-os/main/issues) if you find a problem.

## Verification

These images are signed with sigstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/ublue-os/silverblue-main
```

If you're forking this repo you should [read the docs](https://docs.github.com/en/actions/security-guides/encrypted-secrets) on keeping secrets in github. You need to [generate a new key-pair](https://docs.sigstore.dev/cosign/overview/) with `cosign`. The public key can be in your public repo (your users need it to check the signatures), and you can paste the private key in Settings -> Secrets -> Actions.

### Contributor Metrics

![Main](https://repobeats.axiom.co/api/embed/8c1cbbfa23870f249a1af8abbf8ec5b4dcf5e595.svg "Repobeats analytics image")
