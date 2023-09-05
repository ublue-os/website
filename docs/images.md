# Full Image List

This list is in alphabetical order.

- Images ending in `-main` are suitable for AMD/Intel GPU users
- Images ending in `-nvidia` are suitable for Nvidia GPU users

!!! warning

    If you're coming from an existing Fedora installation **please ensure you remove layered packages before rebasing!** If you're not familiar with the usage of `rpm-ostree` we strongly recommend [reading the documentation](https://coreos.github.io/rpm-ostree/).

## Preparing to Rebase

1. Optional: it is recommended that you pin your current ostree image to make sure you can roll back if you change your mind using:
    ```
   sudo ostree admin pin <index: number>
   ```   
   For example pinning the deployment at index 0 by running `sudo ostree admin pin 0`

2. `rpm-ostree reset` will remove all your layered packages and prepare for rebasing.
3. Ensure your system is up-to-date with an: `rpm-ostree update` and reboot.

## Rebase to an unsigned image first

!!! warning

    You need to run this command, and then reboot. Afterwards

        rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/🚨IMAGE_NAME_HERE🚨

🚨IMAGE_NAME_HERE🚨 examples are `kinoite-main`, `silverblue-main`, `bazzite`, `bluefin-dx`, and so on.

- Nvidia users should check [the NVIDIA README](https://universal-blue.org/images/nvidia/) for important instructions to set up kernel parameters after boot

After you have rebooted, switch to the signed image by running one of the commands below for the image you want. If you're already on the signed image then switching over should be a quick rebase, and then reboot.

## Image List

{!_generated_image_list.md!}
