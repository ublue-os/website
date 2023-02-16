# FAQ

This is a list of some common questions/issues:

## Why is there no installer?

The current Anaconda installer doesn't support installing custom images. Here's the [upstream issue](https://bugzilla.redhat.com/show_bug.cgi?id=2125655). Note that kickstart scripts run in a chroot, so adding a rebase at the end of a kickstart script won't work, we tried that. :) 

For now we recommend reading the [Administrator's Handbook](https://coreos.github.io/rpm-ostree/administrator-handbook/) so that you can learn how to pin, rollback, and switch between images. 

!!! note "Default applications"

    The default applications that are installed depend on which ISO you used to install. Silverblue will come with GNOME apps, and Kinoite will come with KDE apps. These are installed via Flatpak and can be cleanly uninstalled if you prefer something else.

## What's the differences between all these images?

It depends, some are vanilla Fedora with an extra desktop that might not yet be officially supported.
Some modify Fedora in some way, like adding drivers.
And some of them take a more opinionated approach to the final "product" than Fedora does.
Refer to the README of that specific image to learn more about it.

## What should I know about rebasing between images? 

The images provide _system level_ components. Desktops and applications will continue to use your home directory for their data. So for example if you started with Kinoite and rebased to GNOME, then to XFCE, you will have all three of those desktops' dotfiles and configuration in your home directory. This may or may not be important to you depending on your usage, available disk space, and how you manage your personal data. 

!!! note

    Rebasing between images will not affect your installed applications, those are handled by flatpak.

## Why does it download more changes than it seems like it should?

Ideally we'd get one lovely zstd-compressed container diff every day but it's not there yet.
Check out this [upstream issue](https://github.com/coreos/rpm-ostree/issues/4012) for more information on progress in this area.

## What is the relationship between uBlue and Fedora?

uBlue is not officially endorsed or a part of the Fedora project, it's a group of enthusiasts who want to play in this new sandbox that Fedora has created.
This project tends to exercise new features in ostree and Fedora, and as a result we might be the first ones to run into an issue.
We endevaour to be a healthy contributing partner to the Fedora ecosystem, so please be cognizant of that when reporting issues, we want to help where we can!

## I can't find what I want!

It's still early days, as the community grows we expect more images and more awesome stuff.
If you have an idea feel free to post in the [GitHub discussions](https://github.com/orgs/ublue-os/discussions).
