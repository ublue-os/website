 # Making your own Bazzite, Beyond, or Bluefin
 
 Sometimes you don't want to make a whole new image from scratch, you just want to change some things without too much extra work. Sometimes it's nicer to derive from images that more end-user focused like [Bazzite](https://github.com/ublue-os/bazzite), [Beyond](https://github.com/ublue-os/beyond), and [Bluefin](https://github.com/ublue-os/bluefin).
 
 ## Use Cases
 
 - You want to help development by being able to test your contributions prior to submiting to the community.
     - Hardware enablement, experimental features, confirming fixes ahead of merge
 - You want to change out applications and other default choices but want to stick close to Bazzite/Bluefin to get improvements automatically
     - For example, Bluefin DX has Visual Studio baked into the image. If you want the rest of it but don't use vscode you could replace it or remove it. 
     - You need to layer something like VPN software that has to be on an image but you don't want to maintain your own standalone image. (Deriving off of others is always easier, that's why we made this project)
     - You want a personal-use image with config and software changes, but also want to benefit from work being completed upstream.
 
[`ublue-os/main`](https://github.com/ublue-os/main), and [`ublue-os/nvidia`](https://github.com/ublue-os/nvidia) are used to generate base images of everything, so are usually not good candidates for this unless you are familiar with git, containers, and GitHub Actions. Check out the [Setup Guide](/tinker/setup/) if you are interested in generating something from a base image.

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
