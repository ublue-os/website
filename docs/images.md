This list is in alphabetical order. 

- Images ending in `-main` are suitable for AMD/Intel GPU users
- Images ending in `-nvidia` are suitable for NVidia GPU users

!!! warning

    If you're coming from an existing Fedora installation **please ensure you remove layered packages before rebasing!** If you're not familiar with the usage of rpm-ostree we strongly recommend [reading the documentation](https://coreos.github.io/rpm-ostree/).

## Preparing to Rebase

1. `rpm-ostree reset` will remove all your layered packages and prepare for rebasing. 
2. Rebase to an *unsigned* Universal Blue image, this will ensure that you have the proper keys and policies on your machine:

        rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/silverblue-main
   
3. Then reboot, next rebase to a signed image of your choice below: 

## Image List

{!_generated_image_list.md!}
