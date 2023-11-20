---
date: 2023-05-29
comments: true
authors: 
  - bsherman
links:
  - Community Discussion: https://github.com/orgs/ublue-os/discussions/106
  - Akmods: https://github.com/ublue-os/akmods
  - Config: https://github.com/ublue-os/config
  - Main: https://github.com/ublue-os/main
  - Nvidia: https://github.com/ublue-os/nvidia
---

# Akmods Image now Available

Since early in the Universal Blue project, our [Nvidia repository](https://github.com/ublue-os/nvidia) has been building kernel modules(akmods), though only Nvidia drivers. While this approach worked great at first, it became apparent that the akmods would need to be split off into it's own layer: 

![image](https://user-images.githubusercontent.com/1264109/223513413-45c425a4-bd90-4d33-af47-52a4aac70908.png)

This kicked off a nice community discussion where the team figured out an approach.

First we [needed to migrate to a new signing key](https://ublue.it/blog/2023/05/19/important-secure-boot-changes-required-for-nvidia-image-users/) and then begin splitting the akmods into [its own repository](https://github.com/ublue-os/akmods). Conveniently, this also allows us to include things like `v4l2loopback` so that Universal Blue users will have that working out of the box. Soon we hope to add more hardware enablement akmods like XBox Wireless controllers, OpenRazer, and some older Broadcom wireless drivers. 

### Current status:
- The `config` repo provides `just` commands to import the new akmod key AND the older legacy nvidia key
- The `akmods` repo signs kmods with new key (and provides key in an RPM)
- The installer ISO installs BOTH the old and new keys
- The `nvidia` repo is still signing the Nvidia kmods with the old key (and provides both old and new key in RPM)

Sometime on June 17th we will cutover `nvidia` to the new signing key so that existing users can [migrate to the new key ahead of time](https://ublue.it/blog/2023/05/19/important-secure-boot-changes-required-for-nvidia-image-users/). 

## Checking for the v4l2loopback module

You will see the update coming automatically in the background or if you do an `rpm-ostree status`:

    Added:
      kmod-v4l2loopback-6.2.15-300.fc38.x86_64-0.12.7^20230503g2c9b670-1.fc38.x86_64
      ublue-os-akmods-key-0.1-1.fc38.noarch
      v4l2loopback-0.12.7^20230503g2c9b670-1.fc38.x86_64

After you reboot into your new deployment you can double check that the module exists:

    $ ls /lib/modules/`uname -r`/extra
    v4l2loopback


## Special Thanks

This work was patiently prototyped by [@dhoell](https://github.com/dhoell) over the course of many months while juggling a busy school schedule. Thanks for your contribution David!
