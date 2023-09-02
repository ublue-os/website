---
date: 2023-09-02
comments: true
authors: 
  - xynydev
links:
  - ublue-os/startingpoint: https://github.com/ublue-os/startingpoint
  - startingpoint rewrite PR (#135): https://github.com/ublue-os/startingpoint/pull/135
  - Making your own image: https://universal-blue.org/tinker/make-your-own/
---

# Startingpoint rewrite heads-up – What you need to know

Startingpoint, the 'template' repository for creating custom images that includes a simplified configuration format `recipe.yml`, has been going through a rewrite for almost a month now. The rewrite is going to be merged as soon as it and the documentation is ready and tested, and this post will guide you through the changes.

The rewrite brings startingpoint from a single `build.sh` where incrementally added features were piled up, to a collection of modules run by a very simple build script in the order specified in the `recipe.yml` configuration. This fundamental change makes startingpoint more extensible and customizable, allowing you to add and remove features as you please. It also allows for sharing of certain configuration, such as packages lists, between multiple images built in the same repository.

Unfortunately, breaking changes have been made to the configuration (recipe) and the script system.   
For maintainers of custom images, there are a couple of ways to deal with this.
- Create a new repository and port your changes
    - This approach will be easiest if you are not that familiar with `git` and your changes are small.
    - This approach has the advantage that you can keep using your old repository while porting all of your changes to the new one.
    - If your old repository is a fork of startingpoint, you might want to [detach](https://support.github.com/contact?tags=rr-forks&subject=Detach%20Fork&flow=detach_fork) it from startingpoint. This would allow you to fork startingpoint again to create your new repository (GitHub allows only one fork per-repo per-account).
- Do a manual merge of the rewrite into your repository
    - You'll need to be familiar with using some software that allows you to do manual git merges. You want to accept all incoming files that are not configuration files, and manually figure out the configuration files.
    - This approach has the advantage of keeping your git history, and allowing you to easily move all your custom scripts into the new build at once.
- Do nothing
    - Perhaps you've got a great custom build system going, you've done a lot of changes to `build.sh`, you've added new features you need. Or you just can't be bothered? Cool! You don't need to keep up-to-date with the startingpoint template if you don't want to. You'll still get OS updates, your current setup won't break. You just won't be able to take advantage of new features that might get added to startingpoint.

## Ok, but what actually changed?

Take a quick look at the new default `recipe.yml`.
```yml
# image will be published to ghcr.io/<user>/<name>
name: startingpoint
# description will be included in the image's metadata
description: A starting point for further customization of uBlue images. Make your own! https://ublue.it/making-your-own/

# the base image to build on top of (FROM) and the version tag to use
base-image: ghcr.io/ublue-os/silverblue-main
image-version: 38 # latest is also supported if you want new updates ASAP

# list of modules that will be executed in order
# you can include multiple of the same module
modules:
  - type: rpm-ostree
    repos: 
      # - https://copr.fedorainfracloud.org/coprs/atim/starship/repo/fedora-%OS_VERSION%/atim-starship-fedora-%OS_VERSION%.repo
    install:
      - python3-pip # required for yafti
      - libadwaita # required for yafti
    remove:
      - firefox # default firefox removed in favor of flatpak
      - firefox-langpacks # langpacks needs to also be removed to prevent dependency problems

  - type: bling # configure what to pull in from ublue-os/bling
    install:
      - fonts # selection of common good free fonts
      - justfiles # add "!include /usr/share/ublue-os/just/bling.just"
                  # in your custom.just (added by default) or local justfile
      - nix-installer # shell shortcuts for determinate system's nix installers
      - ublue-os-wallpapers
      # - ublue-update # https://github.com/ublue-os/ublue-update
      # - dconf-update-service # a service unit that updates the dconf db on boot
      # - devpod # https://devpod.sh/ as an rpm


  - type: yafti # if included, https://github.com/ublue-os/yafti will be installed and set up
    custom-flatpaks: # this section is optional
      - Celluloid: io.github.celluloid_player.Celluloid
      - Krita: org.kde.krita

  - type: script
    scripts:
      # this sets up the proper policy & signing files for signed images to work
      - signing.sh 
```

You'll see that instead of top-level configuration keys like `rpm:` or `firstboot:`, there's one top-level array `modules:` that includes most of the previous configuration as *modules*. Modules are scripts, executed in the specified order, that take in yaml configuration from the recipe. Anyone can create a module by just putting a script in a subdirectory the `modules/` directory. You can remove modules by just removing the entry in the `modules:` array, you can include multiple of the same type of module, and you can even share modules between recipes (images) using the `- from-file: example.yml` syntax.

This modular system changes the role of scripts a little. Scripts are no longer *intended* to read `recipe.yml`, instead they do a single (or a collection of) commands that are not intended to be configurable in the recipe. If you want to create a script that takes in configuration, create a *module*. Furthermore, scripts in the `pre/` and `post/` directories will no longer be executed by default, as there is no set "pre" and "post" phase with the modular system.

As a minor change, all user configuration has been moved into the `config/` directory in the root of the repository. This might make manual merging from the old version a bit more convoluted, but should ease merges in the future. The whole of the config directory is copied into `/usr/share/ublue-os/startingpoint/` where it's contents can be read on the booted system.

## When can I expect the PR to merge?

When it is fully ready, tested, and documentation changes have been PRd onto the documentation website. A while after the merge there'll be a more newcomer-friendly announcement post. The new version will be considered a '1.0', and the amount of breaking changes will be kept as zero for as long as possible. 
   
For post-release I have plans for a PR that would allow the configuration of _multiple_ modules be included using the `from-file:` syntax, a PR that would allow an entire directory full of build scripts to be run at once, without having to specify each one individually, and a blog post that would showcase high-level technical details of the repository without needing to get in the weeds by reading source code.

Technically, it would also be possible to "reverse" the flow by "compiling" the `recipe.yml` into a `Containerfile`, which is something I'm interested in exploring.