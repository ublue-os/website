# Making your own Bazzite, Beyond, or Bluefin
 
Sometimes you don't want to make a whole new image from scratch, you just want to change some things without too much extra work. Sometimes it's nicer to derive from images that more end-user focused like [Bazzite](https://github.com/ublue-os/bazzite), [Beyond](https://github.com/ublue-os/beyond), and [Bluefin](https://github.com/ublue-os/bluefin).
 
## Use Cases
 
- You want to help development by being able to test your contributions prior to submiting to the community.
    - Hardware enablement, experimental features, confirming fixes ahead of merge
- You want to change out applications and other default choices but want to stick close to Bazzite/Bluefin to get improvements automatically
    - For example, Bluefin DX has Visual Studio baked into the image. If you want the rest of it but don't use vscode you could replace it or remove it. 
    - You need to layer something like VPN software that has to be on an image but you don't want to maintain your own standalone image. (Deriving off of others is always easier, that's why we made this project)
    - You want a personal-use image with config and software changes, but also want to benefit from work being completed upstream.
 
[`ublue-os/main`](https://github.com/ublue-os/main) are used to generate base images of everything, so are usually not good candidates for this unless you are familiar with git, containers, and GitHub Actions. Check out the [Setup Guide](/tinker/setup/) if you are interested in generating something from a base image.

## Instructions
 
1. Fork bazzite/bluefin into your own repo
1. Install: https://wei.github.io/pull/ to your repo and read the docs, be sure to also [star the repo](https://github.com/wei/pull) for higher priority merging by the bot.
1. Follow [the instructions](/tinker/setup/manual/?h=signing#3-set-up-container-signing) for generating a new cosign keypair. Ensure that the `SIGNING_SECRET` and `cosign.pub` file are in the proper places and that your build succeeds before moving on!
1. The config file for the pull app is stored at `.github/pull.yml`, by default it will merge future changes from ublue-os upstream. If you're forking a fork, be sure to change the `upstream` definition in the config.
1. Make your changes:
   - Usually changing package choices, commit them in your repo
   - The bot will create pull requests for your fork as upstream receives changes, and later merge those pull requests automatically, kicking off an automatic build of your forked image.
1. Check the actions tab to monitor the build. Then rebase to your personal image. The package name and URL will be in your packages section of github, like this: https://github.com/castrojo?tab=packages
1. Neat huh? Tell your friends how cool this is. 

## Advanced
If you are a contributor or want to become one in the future, it could be handy to use a more advanced approach. You will have the best of both worlds: being able to contribute to the upstream project and use your own changes.

The following example is based on the `bluefin` project.

1. Create a second branch on your fork called `bluefin-main`
1. Change the `.github/pull.yml` on your `main` branch to keep `bluefin-main` in sync with the upstream branch and merge it with your `main` branch of your fork. Like in the following example:
```
version: "1"
rules:
  - base: bluefin-main
    upstream: ublue-os:main
    mergeMethod: hardreset
    mergeUnstable: false
  - base: main
    upstream: bluefin-main
    mergeMethod: merge
    mergeUnstable: false
label: ":arrow_heading_down: pull"
conflictLabel: "merge-conflict"
```

## Ensuring proper image metadata

### Ublue-update and `image-info.sh`

When forking to create your own image, or using Bluefin as a base image be aware to use the correct values for `image-info.sh`. This script is used to create a file that lives in the container image called `image-info.json`. An example of that file in bluefin-dx shown below stored in `/usr/share/ublue-os/image-info.json`:
```
{
  "image-name": "bluefin-dx",
  "image-flavor": "main",
  "image-vendor": "ublue-os",
  "image-ref": "ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-dx",
  "image-tag":"latest",
  "base-image-name": "",
  "fedora-version": "38"
}
```

This information is used by the [ublue-update service](https://github.com/ublue-os/ublue-update/tree/main/files/usr/lib/systemd), to get unverified installations to automatically rebase to `ostree-image-signed` versions. It is also used by the offline ISO to rebase from a local image to the correct remote one. When you create your own image based on Bluefin, or fork these information must be set up correctly to use your fork. The `image-info.sh` uses variables in the `Containerfile` to write the correct information into the json file. 

```
{
  "image-name": "$IMAGE_NAME",
  "image-flavor": "$IMAGE_FLAVOR",
  "image-vendor": "$IMAGE_VENDOR",
  "image-ref": "$IMAGE_REF",
  "image-tag":"$IMAGE_TAG",
  "base-image-name": "$BASE_IMAGE_NAME",
  "fedora-version": "$FEDORA_MAJOR_VERSION"
}
```

So make sure your Container file has the following in it:

A copy of the `image-info.sh` script to help generate the `image-info.json` file

`COPY image-info.sh /tmp/image-info.sh`

A command to run the `image-info.sh` script

`RUN /tmp/image-info.sh`

Be sure that the variables used in the image-info.sh script are set to the right values. 
```
ARG IMAGE_NAME="${IMAGE_NAME}"
ARG IMAGE_VENDOR="ublue-os"
ARG IMAGE_FLAVOR="${IMAGE_FLAVOR}"
ARG BASE_IMAGE_NAME="${BASE_IMAGE_NAME}"
ARG FEDORA_MAJOR_VERSION="${FEDORA_MAJOR_VERSION}"
```

The IMAGE_VENDOR equals the name of your Github account. In our case we set it to "ublue-os". All the other variables are passed in via build arguments of the container.
