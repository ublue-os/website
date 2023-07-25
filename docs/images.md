This list is in alphabetical order. 

- Images ending in `-main` are suitable for AMD/Intel GPU users
- Images ending in `-nvidia` are suitable for NVidia GPU users

!!! warning

    If you're coming from an existing Fedora installation **please ensure you remove layered packages before rebasing!** If you're not familiar with the usage of rpm-ostree we strongly recommend [reading the documentation](https://coreos.github.io/rpm-ostree/).

## Preparing to Rebase 

1. `rpm-ostree reset` will remove all your layered packages and prepare for rebasing. 
2. Now you need to pull our signing key out of one of our images so that you can rebase to one of ours. This command will do that and then rebase to the image you want in one step. Please ensure you fill in the image part of the URL below with the image name you want to use:

        podman pull ghcr.io/ublue-os/config && rpm-ostree install --assumeyes --apply-live --force-replacefiles $(find ~/.local/share/containers -name ublue-os-signing.noarch.rpm 2>/dev/null) && rpm-ostree rebase --uninstall $(rpm -q ublue-os-signing-* --queryformat '%{NAME}-%{VERSION}-%{RELEASE}.%{Arch}') ostree-image-signed:docker://ghcr.io/ublue-os/🚨IMAGE_NAME_HERE🚨:latest

🚨IMAGE_NAME_HERE🚨 examples are `kinoite-main`, `silverblue-main`, `bazzite`, `bluefin-dx`, and so on. Yes, we know this command is ridiculous. 

- NVidia users should check [the NVIDIA README](https://universal-blue.org/images/nvidia/) for important instructions to set up kernel parameters.
   
## Image List

{!_generated_image_list.md!}
