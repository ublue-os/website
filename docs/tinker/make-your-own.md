# Making your own Bazzite, Beyond, or Bluefin

 Sometimes you don't want to make a whole new image from scratch, you just want to change some things without too much extra work. Sometimes it's nicer to derive from images that more end-user focused like [Bazzite](https://github.com/ublue-os/bazzite), [Beyond](https://github.com/ublue-os/beyond), and [Bluefin](https://github.com/ublue-os/bluefin).

The concept around image-based operating systems balances on the idea that the core image is ready to go, and ideally users don't need to touch it, but we understand that people like to tinker. Instead of layering packages that compromise the integrity of upgrades, we provide the tools for you to make your own image allowing you to have a pristine setup with just the configuration you want with minimal maintenance.

This guide will help you set up your own GitHub repository to build a custom image, using the [`ublue-os/startingpoint`](https://github.com/ublue-os/startingpoint) template. At the end of the guide, you'll have a easily configurable base repository for building and signing a bootable OCI image.

This guide requires you know at least the basics of using `git` and GitHub. If you are not yet familiar with the tools, you should understand some basics, like what a repository is, how committing and pushing work, what branches are, etc. You can start by reading the GitHub documentation [for getting started with git](https://docs.github.com/en/get-started/getting-started-with-git) and [for using git](https://docs.github.com/en/get-started/using-git).

The template is built such that, for simple use cases, you don't need to know any [`Containerfile` syntax](https://docs.docker.com/engine/reference/builder/) or how [GitHub Actions](https://docs.github.com/en/actions) work, or even having much shell scripting experience, but knowing how those tools work will make more advanced modification possible.

## Use Cases

- You want to help development by being able to test your contributions prior to submitting to the community.
  - Hardware enablement, experimental features, confirming fixes ahead of merge
- You want to change out applications and other default choices but want to stick close to Bazzite/Bluefin to get improvements automatically
  - For example, Bluefin DX has Visual Studio baked into the image. If you want the rest of it but don't use vscode you could replace it or remove it. 
  - You need to layer something like VPN software that has to be on an image but you don't want to maintain your own standalone image. (Deriving off of others is always easier, that's why we made this project)
  - You want a personal-use image with config and software changes, but also want to benefit from work being completed upstream.

[`ublue-os/main`](https://github.com/ublue-os/main), and [`ublue-os/nvidia`](https://github.com/ublue-os/nvidia) are used to generate base images of everything, so are usually not good candidates for this unless you are familiar with git, containers, and GitHub Actions. Check out the [Setup Guide](/tinker/setup/) if you are interested in generating something from a base image.

## Instructions

1. [Fork](/tinker/setup/manual/) bazzite/bluefin into your own repo.
2. Install: https://wei.github.io/pull/ to your repo and read the docs, be sure to also [star the repo](https://github.com/wei/pull) for higher priority merging by the bot.
3. Follow [the instructions](/tinker/setup/manual/?h=signing#3-set-up-container-signing) for generating a new cosign keypair. Ensure that the `SIGNING_SECRET` and `cosign.pub` file are in the proper places and that your build succeeds before moving on!
4. The config file for the pull app is stored at `.github/pull.yml`, by default it will merge future changes from ublue-os upstream. If you're forking a fork, be sure to change the `upstream` definition in the config.
5. Make your changes:
   - Usually changing package choices, commit them in your repo
   - The bot will create pull requests for your fork as upstream receives changes, and later merge those pull requests automatically, kicking off an automatic build of your forked image.
6. Check the actions tab to monitor the build. Then rebase to your personal image. The package name and URL will be in your packages section of github, like this: https://github.com/castrojo?tab=packages
7. Neat huh? Tell your friends how cool this is.
