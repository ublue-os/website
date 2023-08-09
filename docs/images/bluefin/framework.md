Bluefin is available as an image for the Framework 13 laptop that comes preconfigured with tlp and the [recommended power settings](https://github.com/ublue-os/bluefin/blob/main/framework/etc/tlp.d/50-framework.conf) from the [Framework Knowledge Base](https://knowledgebase.frame.work/en_us/optimizing-fedora-battery-life-r1baXZh).

Follow the [installation instructions](/installation) - `bluefin-framework` and `bluefin-dx-framework` are available in the boot options in the installer. 

Note that the default image works fine on the Framework 13, this image provides tweaks and further improvements. 

## Changes

Like all Universal Blue images, hardware acceleration and codecs are [included out of the box](/guide/codecs) and the system strives for a zero-maintenance based approach.

- Replaces `power-profiles-daemon` with `tlp`
- Ships the [recommended power profile](https://github.com/ublue-os/bluefin/blob/main/framework/etc/tlp.d/50-framework.conf) for `tlp`
- Sets the text scaling factor in GNOME to [1.25](https://github.com/ublue-os/bluefin/blob/main/framework/etc/dconf/db/local.d/01-ublue-framework)
  - Since Bluefin comes with fractional scaling already enabled by default you may want to adjust those settings, however this will case Electron apps to become blurry. Setting the text font larger seems to be the least worst solution we could come up with.
  - Add's the following kernel arguments: `"module_blacklist=hid_sensor_hub" "nvme.noacpi=1" "tpm_tis.interrupts=0"`
    - Note that kernel arguments are applied after first boot with the command `just framework-13`, see the instructions below

## Additional Diagnostic Tools

- `just benchmark` - will run [stress-ng](https://github.com/ColinIanKing/stress-ng) for 1 minute
- [`powertop`](https://github.com/fenrus75/powertop) - allows you to monitor power consumption in real time

## How to Help!

Open Source succeeds best whene contributors come together to solve a problem. These are areas where contributions would be appreciated:

- Additional `tlp` configurations. The image is designed to allow shipping multiple power profiles, we just need to collect and curate a set that would be the most useful for people
- Benchmarking tools. It would be nice to be able to run a continuous benchmark that exercises the laptop and can run unattended so that we can automate power testing.

We want to allow Linux users to share this knowledge and expertise with each other to fulfill the true potential of the Framework. We'll [use science](https://www.youtube.com/watch?v=BABM3EUo990) and the wonders of modern automation to accomplish this!

And lastly, right now `-framework` is a one-off created for Bluefin. It is entirely feasible for Universal Blue to adopt this across all the base images, but we'd need some help, devops ninjas, inquire within.

- [Thread on the Framework forums](https://community.frame.work/t/custom-fedora-oci-images-for-framework-laptops/34253/) - general feedback welcome here, the co-creator of Bluefin dogfoods this image on a 13th gen Framework 13. Yes, it is glorious. 
- [Contributions welcome!](https://github.com/ublue-os/bluefin)

## Instructions

### Fresh installs

1. Run this command to set the right kernel arguments for the brightness keys to work:
  
        just framework-13

and then reboot one more time! We strive to make that the last piece of operating system maintenance you'll have to do for the life of the machine. 

### Rebasing from another image.

If you're rebasing from another image follow these instructions!

1. Rebase to the -framework image: 

    Bluefin:

        sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-framework:38

    Bluefin Developer Experience:

        sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-dx-framework:38

1. Reboot! 
1. Then run this command to set the right kernel arguments for the brightness keys to work:
  
        just framework-13

Then reboot one more time and you're done!

## Support for various other Framework laptops

The initial release supports the 13th generation Intel Framework 13. It is entirely possible for machine-specific tweaks as part of the image. [Contributions are welcome](/CONTRIBUTING) if you want to enable a specific model. 
