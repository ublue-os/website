This list is in alphabetical order. 

- Images ending in `-main` are suitable for AMD/Intel GPU users
- Images ending in `-nvidia` are suitable for NVidia GPU users

!!! warning

    If you're coming from an existing Fedora installation **please ensure you remove layered packages before rebasing!** If you're not familiar with the usage of rpm-ostree we strongly recommend [reading the documentation](https://coreos.github.io/rpm-ostree/).

## Preparing to Rebase

1. `rpm-ostree reset` will remove all your layered packages and prepare for rebasing/
2. Import the [Universal Blue policy.json](https://raw.githubusercontent.com/ublue-os/config/main/files/usr/etc/containers/policy.json):
   
       sudo curl -L https://github.com/ublue-os/config/raw/main/files/usr/etc/containers/policy.json -o /etc/containers/policy.json`


## Image List

{!_generated_image_list.md!}
