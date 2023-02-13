# Frequently Asked Questions

This is a list of some common questions/issues:

## Why is there no installer?

The current Anaconda installer doesn't support installing custom images. Here's the [upstream issue](https://bugzilla.redhat.com/show_bug.cgi?id=2125655). Note that kickstart scripts run in a chroot, so adding a rebase at the end of a kickstart script won't work, we tried that. :) 

For now we recommend reading the [Administrator's Handbook](https://coreos.github.io/rpm-ostree/administrator-handbook/) so that you can learn how to pin, rollback, and switch between images. 

## What's the differences between all these images?

It depends, some are vanilla Fedora with an extra desktop that might not yet be officially supported.
Some modify Fedora in some way, like adding drivers.
And some of them take a more opinionated approach to the final "product" than Fedora does.
Refer to the README of that specific image to learn more about it.

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