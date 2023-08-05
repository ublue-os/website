# Bluefin Administration

## Management (Todo)

Bluefin includes Cockpit for machine management. We're hoping to include more out of the box management templates, please file an issue if you're interested in helping complete this feature

## Verification

These images are signed with sigstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command:

    cosign verify --key cosign.pub ghcr.io/ublue-os/bluefin
    
## Building Locally

1. Clone this repository and cd into the working directory

       git clone https://github.com/ublue-os/bluefin.git
       cd bluefin

1. Make modifications if desired
    
1. Build the image (Note that this will download and the entire image)

       podman build . -t bluefin
    
1. [Podman push](https://docs.podman.io/en/latest/markdown/podman-push.1.html) to a registry of your choice.
1. Rebase to your image to wherever you pushed it:

       sudo rpm-ostree rebase ostree-image-signed:docker://whatever/bluefin:latest
   
