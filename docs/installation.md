# Installation

Check out the [upstream installation documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) for more information.

Notably:

- Dual boot configurations are not supported. We recommend using your PC's BIOS/UEFI boot menu for dual boot configuration so that each OS has its own disk.
- Manual partitioning is not supported.

## Bazzite

Bazzite is a custom image built on Fedora Atomic technology that brings the best of Linux gaming to all of your devices (yep, even your favorite handheld). Featuring a rock-solid base with automatic updates and ninety days of rollbacks.

- Check [the Bazzite image picker](https://bazzite.gg#image-picker) for download instructions

## Bluefin

The next generation Linux workstation, designed for reliability, performance, and sustainability.

- Check [the Bluefin documentation](https://universal-blue.discourse.group/docs?topic=41) for image download instructions

## Generating your own custom ISO of a main image

Use any machine with `docker` to generate an ISO of a main image:

    docker run --rm --privileged --volume .:/isogenerator/output -e VERSION=39 -e IMAGE_NAME=kinoite-nvidia -e IMAGE_TAG=latest -e VARIANT=Silverblue ghcr.io/ublue-os/isogenerator:39

You can find the list of published images on [the GitHub packages page](https://github.com/orgs/ublue-os/packages)

Check the [isogenerator documentation](https://github.com/ublue-os/isogenerator) for more information on generating your own ISO image.

 

