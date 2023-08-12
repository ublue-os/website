# Bluefin Administration

## Day to Day Operation

### System Updates

Bluefin is designed to be "hands off". System updates apply once a day and Flatpaks update twice a day [in the background](https://github.com/ublue-os/config/tree/main/files/usr/lib/systemd). Updates are applied when the system reboots, therefore it is recommended to just regularly power off your device when it's not being used to ensure kernel updates are being applied. Application updates (like the browser) happen independently of this and don't require a reboot.

See [configuration of updates](/faq/#how-do-i-configure-automatic-updates) if you want to change the default behavior. 

Machine firmware updates are provided through the standard Software Center:

![Firmware updates](https://github.com/ublue-os/website/assets/1264109/b6706ae4-d519-4508-b350-defce27aa8e4)

## Installing Applications

Use the GNOME Software Center to [install applications from Flathub](https://flathub.org/). Unlike stock Fedora, system updates and upgrades are not handled by this application, it's scope has been reduced to only install Flatpaks from Flathub.

![GNOME Software Center](https://github.com/ublue-os/website/assets/1264109/86e06ae4-0aec-46ef-9709-936c3e938f70)


## Upgrades and Throttle Settings

!!! Info "This feature is incomplete"

Bluefin is available with two throttle settings. 

The latest stable release of Fedora is always tagged `latest`. The still-supported but older release is labelled as `gts`, which is slang for "Grand Touring Series`, for those who wish to enjoy the ride from a slower cadence. It is the default Bluefin experience starting with Fedora 39. 

Explicit version tags of the Fedora release are available for users who wish to manually handle their upgrade cycle:

To lock to Fedora 39

     sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin:39

To always be on the latest stable release:

     sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin:latest

Additionally rebasing to a specific date tag is encouraged if you need to "pin" to a specific day or version:

    sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin:38-20231101

Check the [Fedora Silverblue User Guide](https://docs.fedoraproject.org/en-US/fedora-silverblue/) for more information. 

## Remote Management

!!! Info "This feature is incomplete"

Bluefin includes Cockpit for machine management. We're hoping to include more out of the box management templates, please [check this issue](https://github.com/ublue-os/bluefin/issues/271) if you're interested in volunteering. 

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
   
