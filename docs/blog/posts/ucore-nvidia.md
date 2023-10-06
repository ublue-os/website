---
date: 2023-10-06
comments: true
authors: 
  - bsherman
links:
  - ucore Commits: https://github.com/ublue-os/ucore/commits/main
---
# Universal Core Gains NVIDIA Support

Universal Core is a Universal Blue custom image of Fedora CoreOS. 

While Universal Blue has been receiving much attention on the desktop; [Universal Core (ucore)](https://github.com/ublue-os/ucore) has been quietly growing its own set of features for the server side of things.

## Announcing NVIDIA Support

Today we get to announce a long awaited feature:  **ucore finally has images available with Nvidia drivers built in!** 

As one of our [oldest feature requests](https://github.com/ublue-os/ucore/issues/18), which also happend to be created on April 1st, some probably wondered if it was an April Fools Day joke. But no, 6 months later, the feature has landed.

### NVIDIA for a Homelab

What could this feature provide a CoreOS/ucore user with an NVIDIA card?

Typically its going to be one of:
- [CUDA](https://developer.nvidia.com/cuda-gpus) for AI, or other GPU accelerated workloads
- [transcoding video](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new) is quite popular, especially if you don't have a later gen Intel CPU with QuickSync


[FrigateNVR](https://frigate.video) is a great example of a self-hostable open source project which can use both [video transcode](https://docs.frigate.video/configuration/hardware_acceleration#nvidia-gpus) capabilities and [compute](https://docs.frigate.video/configuration/detectors#nvidia-tensorrt-detector) capabilities to power a smart home camera solution.


### Details

So, what's actually included with this "nvidia release"?

1. [nvidia kernel driver](https://negativo17.org/nvidia-driver)
    - We pre-build the [latest nvidia driver (kmod)](https://github.com/negativo17/nvidia-driver/blob/master/nvidia-driver.spec) from [negativo17's fedora-nvidia repository](https://negativo17.org/repos/fedora-nvidia.repo).
    - This upstream was chosen over rpmfusion due to its granular packaging concept which allows the installation of only minimal `nvidia-driver-cuda` packages and does NOT require xorg/wayland/etc as dependencies.
2. [nvidia-container-toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/sample-workload.html)
    - CoreOS is focussed on container workloads, and to use NVIDIA on containers, you need their toolkit.
    - The latest version is installed here which simultaneously supports both root and rootless containers. 
    - Both podman and docker can be used.
3. [nvidia container selinux policy](https://github.com/NVIDIA/dgx-selinux/tree/master/src/nvidia-container-selinux)
    - NVIDIA's toolkit docs give examples of running with SELinux disabled on the container: `podman run --security-opt label=disable --device=nvidia.com/gpu=all ubuntu nvidia-smi` but some users may want more security.
    - This policy can preserve other SELinux protections while still providing access to the GPU: `podman run --security-opt label=type:nvidia_container_t --device=nvidia.com/gpu=all ubuntu nvidia-smi` 


#### Older GPUs

If you need an older (or different) driver, [there are other ways](https://github.com/ublue-os/ucore#other-nvidia-drivers) to install a driver. Our approach is meant to be the easiest for the widest group of users.

## Non-NVIDIA Features

Universal Core has plenty to offer even if you don't run NVIDIA GPUs in your server, or even if you want to run in a virtual machine!

Here's a quick summary of what we have to offer:

`ucore` images add the following to CoreOS:
  - [cockpit](https://cockpit-project.org) - GUI for managing the server
  - [distrobox](https://github.com/89luca89/distrobox)
  - guest VM agents (`qemu-guest-agent` and `open-vm-tools`)
  - moby-engine(docker), docker-compose and podman-compose
  - [tailscale](https://tailscale.com) and [wireguard-tools](https://www.wireguard.com)
  - [tmux](https://github.com/tmux/tmux/wiki/Getting-Started)
  - *optionally*
    - [NVIDIA](#details)
    - [ZFS](https://openzfs.github.io/openzfsdocs/Getting%20Started/Fedora/index.html)

`ucore-hci` builds upon `ucore` to provide "hyper-converged infrastructure". These images add more hardware/driver support, more storage tools, and virtualization(hypervisor) support:
  - [cockpit-machines](https://github.com/cockpit-project/cockpit-machines): Cockpit GUI for managing virtual machines
  - intel wifi firmware - CoreOS omits this despite including atheros wifi firmware
  - [libvirt](https://libvirt.org/): libvirt KVM hypervisor management daemon and client tools
  - [mergerfs](https://github.com/trapexit/mergerfs)
  - [snapraid](https://www.snapraid.it/)
  - udev rules enabling full functionality on some [Realtek 2.5Gbit USB Ethernet](https://github.com/wget/realtek-r8152-linux/) devices

## Testers Wanted!

There's still feature requests in the pipeline and opportunities to contribute. Just using `ucore` and providing feedback is incredibly helpful!

If you are interested in using something like Universal Blue, but on a server, [take a look at ucore today](https://github.com/ublue-os/ucore).