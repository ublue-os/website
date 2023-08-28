# uBlue Images (main/nvidia)

When people refer to "uBlue" they will likely mean this:

- Daily, automatic ingestion of [Fedora OSTree desktops](https://quay.io/organization/fedora-ostree-desktops/).
    - Silverblue, Kinoite, Vauxite, Sericea, and others.
    - Additionally MATE and LXQt are provided since Fedora does not offer these images.
    - Continuously built and delivered via an OCI container from a registry (currently ghcr.io).
- Focus on things that Fedora CANNOT ship:
    - Hardware enablement,
    - Non-free codecs aka "a bunch of that RPMFusion stuff,"
    - Built in Nvidia drivers with multiple version support.
- Quality of Life Services:
    - Automatic Updates,
      - System set to auto stage updates,
      - Flatpaks set to auto update.
    - Additional udev rules for better [controller support](https://github.com/ublue-os/config#udev-rules) and 2FA keys.
- Main and Nvidia are "Light Touch:"
    - They are intended to be close(ish) to Fedora.
    - Exceptions to this may granted if multiple maintainers agree based on community feedback in an issue.
      - If an application is available as a Flatpak it will NOT be included.
      - If it works in a Distrobox: SHOULD NOT be included.
      - If it only works on the host AND is required for hardware functionality: SHOULD be included.
    - Kernel modules MUST NOT be included, they are added to `ublue-os/akmods` and `ublue-os/nvidia`.
    - If it only works on the host AND IS NOT required for hardware functionality: MAY be included.

# Universal Blue Toolkit

- The actions and scripts we use to make the Universal Blue images should be designed for consumption by others so that they can make whatever they want.
- [Starting Point](https://github.com/ublue-os/startingpoint) is the repo designed to be cloned.
- Both the toolkit and the images are a work in progress; we're kind of "building the bridge while we're crossing the river," so, we need volunteers here who are willing to experiment.
- Special consideration for existing open source projects that consume Fedora:
    - We want to enable orgs like asus-linux, linux-surface, Framework laptops, etc. to end up on vanilla Fedora, we should act as an unofficial playground for them to prototype, and be flexible enough to want to work with us to just fix the stuff they need. I want to explicitly say "base off of us" if it gets people working computers. If it works, we act as an on ramp for Fedora.
    - We should help them enable their repos if they want to do custom images; don't force them to come here and integrate, if they want to start on our images and then do their own thing, cool, whatever, just give people working computers --- by now everyone knows the sustainable way is by working upstream.

# Project Scope

- Focus on long-term sustainability of the installation:
    - A fraction of a computer's life is day 0-3, we purposely invest in the idea that this installation should last for the life of the hardware
- We should be **brutal** about making things out of scope. We're not going to do extra work for no reason, as SRE/cloud-native people we will **embrace** being lazy and automating the world, not writing custom installers to partition people's disks, we ain't got time for that.
    - If we have to make a thing, it's because we have no choice, and if we do have to make it, we're not happy about it.
    - But we want to experiment too, hence [Fleek](https://getfleek.dev/), [Yafti](https://github.com/ublue-os/yafti), and [Boxkit](https://github.com/ublue-os/boxkit).

## Bazzite, Bluefin, LXQt, and MATE

These images are "Hello World" examples of deriving from the `ublue-os/main` and `ublue-os/nvidia`. They offer stronger opinions and choices.

LXQt and MATE are not offered by Fedora and are built to provide images for those communities.
