# Full Image List

This list is in alphabetical order.

- Images ending in `-main` are suitable for AMD/Intel GPU users
- Images ending in `-nvidia` are suitable for Nvidia GPU users

!!! warning

    If you're coming from an existing Fedora installation **please ensure you remove layered packages before rebasing!** If you're not familiar with the usage of `rpm-ostree` we strongly recommend [reading the documentation](https://coreos.github.io/rpm-ostree/).

## Preparing to Rebase

1. Optional: it is recommended that you pin your current ostree image to make sure you can roll back if you change your mind using:

    ```sh
   sudo ostree admin pin <index: number>
   ```

   For example pinning the deployment at index 0 by running `sudo ostree admin pin 0`

2. `rpm-ostree reset` will remove all your layered packages and prepare for rebasing.
3. Ensure your system is up-to-date with an: `rpm-ostree update` and reboot.

## Rebase to an unsigned image first

!!! warning

    You need to run this command, and then reboot afterwards:

        rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/🚨IMAGE_NAME_HERE🚨

🚨IMAGE_NAME_HERE🚨 examples are `kinoite-main`, `silverblue-main`, `bazzite`, `bluefin-dx`, and so on.

- Nvidia users should check [the NVIDIA README](https://universal-blue.org/images/nvidia/) for important instructions to set up kernel parameters after boot

After you have rebooted, switch to the signed image by running one of the commands below for the image you want. If you're already on the signed image then switching over should be a quick rebase, and then reboot.

## Image Categorization

- Featured Images
  - [Bluefin](https://github.com/ublue-os/bluefin)
  - [Bazzite](https://github.com/ublue-os/bazzite/)
  - [Beyond](https://github.com/ublue-os/beyond)
- Opinionated Fedora Silverblue Images
  - More information on changes from stock Fedora Silverblue [here](/images/main/).
  - Offers different desktop environments and window managers if desired.
  - Download the ISO for all different desktop variants [here](https://github.com/ublue-os/main/releases).
- Specialized Hardware
  - Unique images for specific hardware (Framework, Surface, etc.)
  - Overlaps with the other images.
    - `bazzite-framework` as an example.
- [Community Images](https://universal-blue.discourse.group/t/list-of-community-created-custom-images/340)
  - You can make your own too!  Check out [Making Your Own](/tinker/make-your-own/) and [Forking Your Own](/guide/fork-your-own/).
- Other images
  - Base images that include only the necessary Fedora packages as a starting point.
  - Images without kernel modules or kernel packages.
  - Images intended only for use inside of another image and **not** installed by itself on a desktop.

## Image List

{!_generated_image_list.md!}
