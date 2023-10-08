# Framework Computers (Intel only)

Universal Blue images are available for the Framework 13 laptop. It comes preconfigured with tlp and the [recommended power settings](https://github.com/ublue-os/framework/blob/main/system_files/shared/usr/etc/tlp.d/50-framework.conf) from the [Framework Knowledge Base](https://knowledgebase.frame.work/en_us/optimizing-fedora-battery-life-r1baXZh).

!!! info "Important information for AMD-based sytems" 

    Framework recommends NOT using `tlp` on the new AMD-based Framework 13. These images use `tlp`, so it is currently recommended to use the non-framework images if you own an AMD Framework 13. Check the [community thread](https://community.frame.work/t/announcement-linux-on-your-framework-laptop-13-amd-ryzen-7040-series/37367/36) for the latest information.

Follow the [installation instructions](/installation) to select a Framework image. These images end with `-framework` in their name. 

Note that the default image work fine on the Framework 13, these images provide tweaks and further improvements and are optional for people who prefer to use `tlp`. These images will also work fine on non-Framework laptops.

- [ublue-os/framework](https://github.com/ublue-os/framework) - repository for generating these images

## Changes

Like all Universal Blue images, hardware acceleration and codecs are [included out of the box](/guide/codecs) and the system strives for a zero-maintenance based approach.

- Replaces `power-profiles-daemon` with `tlp`
- Ships the [recommended power profile](https://github.com/ublue-os/framework/blob/main/system_files/shared/usr/etc/tlp.d/50-framework.conf) for `tlp`
- Sets the text scaling factor in GNOME to [1.25](https://github.com/ublue-os/framework/blob/main/system_files/silverblue/usr/etc/dconf/db/local.d/01-ublue-framework)
  - Some images (like Bluefin) come with fractional scaling already enabled by default. You may want to adjust those settings, however this will case Electron apps to become blurry. Setting the text font larger seems to be the "least-worst" solution available.
- Add's the following kernel arguments: `"module_blacklist=hid_sensor_hub" "nvme.noacpi=1" "tpm_tis.interrupts=0"`
  - Note that kernel arguments are applied with the command `just framework-13` and a subsequent reboot. See the [instructions](# instructions) below.

## Additional Diagnostic Tools

- `just benchmark` - will run [stress-ng](https://github.com/ColinIanKing/stress-ng) for 1 minute
- [`powertop`](https://github.com/fenrus75/powertop) - allows you to monitor power consumption in real time

## How to Help

Open Source succeeds best when contributors come together to solve a problem. These are areas where contributions would be appreciated:

- Additional `tlp` configurations. The image is designed to allow shipping multiple power profiles; we just need to collect and curate a set that would be the most useful for people.
- Benchmarking tools. It would be nice to be able to run a continuous benchmark that exercises the laptop and can run unattended so that we can automate power testing.

We want to allow Linux users to share this knowledge and expertise with each other to fulfill the true potential of Framework laptops. We'll [use science](https://www.youtube.com/watch?v=BABM3EUo990) and the wonders of modern automation to accomplish this!

- [Thread on the Framework forums](https://community.frame.work/t/custom-fedora-oci-images-for-framework-laptops/34253/) - general feedback welcome here, the co-creator of Bluefin "dog-foods" this image on a 13th gen Framework 13. Yes, it is glorious.
- [Contributions welcome!](https://github.com/ublue-os/bluefin)

## Instructions

### Fresh installs

Run this command to set the right kernel arguments for the brightness keys to work:
  
```bash
just framework-13
```

and then reboot one more time! We strive to make that the last piece of operating system maintenance you'll have to do for the life of the machine.

### Rebasing from another image

If you're rebasing from another image follow these instructions!

1. Rebase to the `-framework` image:

    Bluefin:

    ```bash
    sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-framework:38
    ```

    Bluefin Developer Experience:

    ```bash
    sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-dx-framework:38
    ```

2. Reboot!
3. Then run this command to set the right kernel arguments for the brightness keys to work:
  
    ```bash
    just framework-13
    ```

4. Then reboot one more time and you're done!

## Support for various other Framework laptops

The initial release supports the 13th generation Intel Framework 13. It is entirely possible for machine-specific tweaks to be added as part of the image. [Contributions are welcome](/CONTRIBUTING) if you want to enable a specific model.

## Contributor Metrics

![Framework](https://repobeats.axiom.co/api/embed/e3129d64593dc0d96aa244d1fd5beb8e9315d381.svg "Repobeats analytics image")
