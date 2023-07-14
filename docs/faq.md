# FAQ

This is a list of some common questions/issues:

We recommend reading the [Administrator's Handbook](https://coreos.github.io/rpm-ostree/administrator-handbook/) so that you can learn how to pin, rollback, and switch between images. 

!!! note "Default applications"

    The default applications that are installed depend on which ISO you used to install. Silverblue will come with GNOME apps, and Kinoite will come with KDE apps. These are installed via Flatpak and can be cleanly uninstalled if you prefer something else.

## What's the differences between all these images?

It depends, some are vanilla Fedora with an extra desktop that might not yet be officially supported.
Some modify Fedora in some way, like adding drivers.
And some of them take a more opinionated approach to the final "product" than Fedora does.
Refer to the README of that specific image to learn more about it.

The images in the [Toolbox section](https://ublue.it/toolboxes/) are meant to be used with [Toolbx](https://containertoolbx.org/) and [Distrobox](https://github.com/89luca89/distrobox).
They are meant to be the used for a command line experience for developers and advanced users.
Please refer to the documentation for those respective projects.

## What should I know about rebasing between images? 

The images provide _system level_ components.
Desktops and applications will continue to use your home directory for their data.
So for example if you started with Kinoite and rebased to GNOME, then to XFCE, you will have all three of those desktops' dotfiles and configuration in your home directory.
This may or may not be important to you depending on your usage, available disk space, and how you manage your personal data. 

!!! note

    Rebasing between images will not affect your installed applications, those are handled by Flatpak.
    
## Isn't this just another immutable Linux distribution?

Fedora Silverblue, Kinoite, Sericea, and many other projects are all often called immutable Linux distributions.
We think that it is a misleading term with the connotation of the end user losing their power.  
To us, the ideas espoused by so-called immutable distributions mean increased stability through separating the stable core from the programs added by the user. The existence of Universal Blue proves that that stable core is not unchangeable. 

Universal Blue is not really even a distribution, it's more a community seeking to augment Fedora Silverblue and it's peers,and giving you the tools to do it too.

## Why are you making another distro?

This isn't a distribution, you can always rebase back to Fedora without reinstalling.
This is a unique relationship between an upstream and downstream that is popular in cloud, but still new to the Linux desktop.
"Custom images" seems to be a decent place to start since that's what people call them in cloud.

## Why does it download more changes than it seems like it should?

Ideally we'd get one lovely zstd-compressed container diff every day but it's not there yet.
Check out this [upstream issue](https://github.com/coreos/rpm-ostree/issues/4012) for more information on progress in this area.

## What is the relationship between Universal Blue and Fedora?

Universal Blue is not officially endorsed or a part of the Fedora project, it's a group of enthusiasts who want to play in this new sandbox that Fedora has created.
This project tends to exercise new features in ostree and Fedora, and as a result we might be the first ones to run into an issue.
We endevaour to be a healthy contributing partner to the Fedora ecosystem, so please be cognizant of that when reporting issues, we want to help where we can!

## How do I configure automatic updates?

!!! warning

    Disabling automatic updates is an unsupported configuration.

With that said, you can individually disable which automatic update timers [ublue-os/config](https://github.com/ublue-os/config) provides with the following commands:

* flatpak system: `sudo systemctl disable flatpak-system-update.timer`
* flatpak user: `sudo systemctl --global disable flatpak-user-update.timer`

You can also configure automatic `rpm-ostree` updates by editing `/etc/rpm-ostreed.conf` and changing "AutomaticUpdatePolicy" to "none" or "check":

```
[Daemon]
AutomaticUpdatePolicy=check
```

### How do I use tools that expect Docker to be available?

Some tools (like `docker-compose`) expect to talk to the Docker socket. Check the Podman documentation for more information on setting this up: 

- [Podman Socket Activation](https://github.com/containers/podman/blob/main/docs/tutorials/socket_activation.md)

## I can't find what I want!

It's still early days, as the community grows we expect more images and more awesome stuff.
If you have an idea feel free to post in the [GitHub discussions](https://github.com/orgs/ublue-os/discussions).
