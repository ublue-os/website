# Making your own image

The concept around image based operating systems balances on the idea that the core image is ready to go, and ideally users don't need to touch it, but we understand that people like to tinker. Instead of layering packages that compromise the integrity of upgrades, we provide the tools for you to make your own image allowing you to have a pristine setup with just the configuration you want with minimal maintenance.

This guide will help you set up your own GitHub repository to build a custom image, using the [`ublue-os/startingpoint`](https://github.com/ublue-os/startingpoint) template. At the end of the guide, you'll have a easily configurable base repository for building and signing a bootable OCI image.

This guide requires you know at least the basics of using `git` and GitHub. If you are not yet familiar with the tools, you should understand some basics, like what is a repository, committing and pushing, what are branches, etc. You can start from reading the GitHub documentation [for getting started with git](https://docs.github.com/en/get-started/getting-started-with-git) and [for using git](https://docs.github.com/en/get-started/using-git).

The template is built such that for simple use cases you don't need to know any [`Containerfile` syntax](https://docs.docker.com/engine/reference/builder/) or how [GitHub Actions](https://docs.github.com/en/actions) work, or even having much shell scripting experience, but knowing how those tools work will make more advanced modification possible. 

[Next up: Get in the right mindset](/tinker/1-mindset/){ .md-button }