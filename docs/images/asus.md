# Microsoft Surface Images

From the [asus-linux.org project](https://asus-linux.org/)

> Asus-Linux.org is an independent community effort that works to improve Linux support for Asus notebooks.

- [ublue-os/asus](https://github.com/ublue-os/asus) - repository for generating these images

## Changes

Like all Universal Blue images, hardware acceleration and codecs are [included out of the box](/guide/codecs) and the system strives for a zero-maintenance based approach.

- Replaces the stock Fedora kernel with the [lukenukem/asus-kernel](https://copr.fedorainfracloud.org/coprs/lukenukem/asus-kernel/)
- Installs the [`asusctl`](https://asus-linux.org/asusctl/) tool
- Installs `fprintd`

## How to Help

Open Source succeeds best when contributors come together to solve a problem. These are areas where contributions would be appreciated:

- Additional `tlp` configurations. The image is designed to allow shipping multiple power profiles; we just need to collect and curate a set that would be the most useful for people.
- Benchmarking tools. It would be nice to be able to run a continuous benchmark that exercises the laptop and can run unattended so that we can automate power testing.

We want to allow Linux users to share this knowledge and expertise with each other to fulfill the true potential of Surface devices. We'll [use science](https://www.youtube.com/watch?v=BABM3EUo990) and the wonders of modern automation to accomplish this!

## Instructions

### Fresh installs


### Rebasing from another image

If you're rebasing from another image follow these instructions!

### Contributor Metrics

![Asus](https://repobeats.axiom.co/api/embed/143fe83d745d0c4d9d5b8d0cd6066bf3b77f8a27.svg "Repobeats analytics image")