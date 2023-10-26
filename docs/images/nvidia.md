# Nvidia

[![build-ublue](https://github.com/ublue-os/nvidia/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/nvidia/actions/workflows/build.yml)

The purpose of these images is to provide [community Fedora images](https://github.com/ublue-os/main) with Nvidia drivers built-in. This approach can lead to greater reliability as failures can be caught at the build level instead of the client machine. This also allows for individual sets of images for each series of Nvidia drivers, allowing users to remain current with their OS but on an older, known working driver. Performance regression with a recent driver update? Reboot into a known-working driver after one command. That's the goal!

These images are based on the experimental `ostree` native container images hosted at [quay.io](https://quay.io/organization/fedora-ostree-desktops) ([repo](https://gitlab.com/fedora/ostree/ci-test)).

!!! Note
    This project is a work-in-progress. You should at a minimum be familiar with the [Fedora documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/) on how to administer an `ostree` system.

## Core image features

- Multiple Nvidia driver streams (535xx and 470xx)
- CUDA support
- [Container runtime support](#using-nvidia-gpus-in-containers)
- Secure boot
- [Hardware-accelerated video playback](#video-playback)
- Selinux support
- [Multiple Fedora flavors and releases](#setup)
- Post-install setup with [`just`](https://github.com/ublue-os/config/blob/main/build/ublue-os-just/40-nvidia.just)
- Multi-GPU support with [`supergfxctl`](https://gitlab.com/asus-linux/supergfxctl) ([optional Gnome Shell extension](https://extensions.gnome.org/extension/5344/supergfxctl-gex/))

## Setup

### 1. Installation

Check the [installation instructions](/installation) for fresh installations.
Use the [images documentation](/images) for rebase instructions.

### 2. Set kargs after rebasing

Use this only if you are rebasing, fresh installations can skip this step.
Setting kargs to disable nouveau and enabling nvidia early at boot is [currently not supported within container builds](https://github.com/coreos/rpm-ostree/issues/3738).
They must be set after rebasing:

```bash
rpm-ostree kargs \
    --append=rd.driver.blacklist=nouveau \
    --append=modprobe.blacklist=nouveau \
    --append=nvidia-drm.modeset=1
```

And then reboot one more time!

### 3. Enable Secure Boot support

!!! Note "**IMPORTANT NOTE:**"
    On June 17, 00:00 UTC, we changed the key used to sign nvidia kernel modules. If your nvidia kernel modules are not loading, you need to import the new key.

[Secure Boot](https://rpmfusion.org/Howto/Secure%20Boot) support for the nvidia kernel modules can be enabled by enrolling the signing key:

```bash
sudo mokutil --import /etc/pki/akmods/certs/akmods-ublue.der
```

Alternatively, the key can be enrolled from within this repo:

```bash
sudo mokutil --import ./certs/public_key.der
```

## Rolling back and rebasing

Generally you can [perform a rollback](https://docs.fedoraproject.org/en-US/fedora-silverblue/updates-upgrades-rollbacks/#rolling-back) with the following:

```bash
rpm-ostree rollback
```

To rebase onto a specific date, use a date tag:

```bash
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/silverblue-nvidia:20230720
```

Or to rebase onto a specific release, driver, and date:

```bash
rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/silverblue-nvidia:38-535-20230720
```

[More options for image tags can be found on the container catalog.](https://github.com/ublue-os/nvidia/pkgs/container/silverblue-nvidia/versions)

## Support

!!! Note
    The Fedora release and Nvidia version can be set with the image tag as well (see table below). Some **older Nvidia cards** (GTX 700 series or older) **REQUIRE** Driver version `470`.

   |     | 535xx series (latest, best supported) | 470xx series (Kepler 2012-2014 support) |
   |-----|---------------------------------------|-----------------------------------------|
   | F37 | :37 / :37-535 / :37-current | :37-470 |
   | F38 | :latest / :38 / :38-535 / :38-current | :38-470 |
   | F39 | :latest / :39 / :39-535 / :39-current | :39-470 |

!!! Warning "Driver Support Subject to Change"
    - Drivers are provided by Nvidia and packaged by RPMFusion, therefore we cannot make any guarantees on support outside of the support these two organizations provide.
    - Due to the nature of third party kernel modules, support for older versions is best effort.
    - It is *strongly encouraged* for you to subscribe to [the Nvidia driver announcements](https://github.com/orgs/ublue-os/discussions/categories/nvidia-driver-announcements?discussions_q=is%3Aopen+category%3A%22Nvidia+Driver+Announcements%22) section of the forums to keep up with the latest changes and news.

!!! Info "TL;DR:"
    We do the best we can but sometimes need to drop support depending on what's going with Nvidia, RPMFusion, Fedora, and/or the Linux kernel.

## Verification

These images are signed with sigstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/ublue-os/silverblue-nvidia
```

If you're forking this repo you should [read the docs](https://docs.github.com/en/actions/security-guides/encrypted-secrets) on keeping secrets in github. You need to [generate a new keypair](https://docs.sigstore.dev/cosign/overview/) with cosign. The public key can be in your public repo (your users need it to check the signatures), and you can paste the private key in Settings -> Secrets -> Actions with the name SIGNING_SECRET.

## Building locally

1. Build container

    A container build can be invoked by simply running:

    ```bash
    podman build \
        --file build.Containerfile \
        --tag build-test:latest
    podman build \
        --file install.Containerfile \
        --tag install-test:latest
    ```

    Or, to specify the version of Fedora and/or Nvidia driver, run:

    ```bash
    podman build \
        --build-arg IMAGE_NAME=silverblue \
        --build-arg FEDORA_MAJOR_VERSION=37 \
        --build-arg NVIDIA_MAJOR_VERSION=525 \
        --file build.Containerfile \
        --tag build-test:37-525

    podman build \
        --build-arg IMAGE_NAME=silverblue \
        --build-arg FEDORA_MAJOR_VERSION=37 \
        --build-arg NVIDIA_MAJOR_VERSION=525 \
        --build-arg AKMODS_CACHE=build-test \
        --build-arg AKMODS_VERSION=37 \
        --file install.Containerfile \
        --tag build-test:latest
    ```

2. Generate signing keys

    If you are forking this repo, then you should add a private key to the repository secrets:

    ```bash
    ./generate-akmod-key
    gh secret set AKMOD_PRIVKEY < certs/private_key.priv.prod
    cp certs/public_key.der.prod certs/public_key.der
    ```

## Using Nvidia GPUs in containers

[There is support for enabling Nvidia GPUs in containers](https://www.redhat.com/en/blog/how-use-gpus-containers-bare-metal-rhel-8). This can can be verified by running the following:

```bash
podman run \
    --user 1000:1000 \
    --security-opt=no-new-privileges \
    --cap-drop=ALL \
    --security-opt label=type:nvidia_container_t  \
    --device=nvidia.com/gpu=all \
    docker.io/nvidia/samples:vectoradd-cuda11.2.1
```

## Video playback

Additional runtime packages are added for enabling hardware-accelerated video playback. This can the enabled in Firefox (RPM or flatpak) by setting the following options to `true` in `about:config`:

- `gfx.webrender.all`
- `media.ffmpeg.vaapi.enabled`
- `widget.dmabuf.force-enabled`

RPM users will need to run Firefox with the following environment variables to use `/usr/lib64/dri/nvidia_drv_video.so`:

```
env LIBVA_DRIVER_NAME=nvidia MOZ_DISABLE_RDD_SANDBOX=1 NVD_BACKEND=direct firefox
```

Flatpak users will also need to provide more extensive host access and reduced sand-boxing:

```bash
flatpak override \
    --user \
    --filesystem=host-os \
    --env=LIBVA_DRIVER_NAME=nvidia \
    --env=LIBVA_DRIVERS_PATH=/run/host/usr/lib64/dri \
    --env=LIBVA_MESSAGING_LEVEL=1 \
    --env=MOZ_DISABLE_RDD_SANDBOX=1 \
    --env=NVD_BACKEND=direct \
    --env=MOZ_ENABLE_WAYLAND=1 \
    org.mozilla.firefox
```

You can verify whether the GPU is being used for video decoding by running `nvidia-smi dmon` while the video is playing.

## Acknowledgements

Thanks to Alex Diaz for advice, and who got this working first, check out this repo:

- <https://github.com/akdev1l/ostree-images>

### Contributor Metrics

![Nvidia](https://repobeats.axiom.co/api/embed/379e3a6bc4de129c152be1a5e80246ae6542208f.svg "Repobeats analytics image")