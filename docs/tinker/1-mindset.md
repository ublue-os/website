# Getting in the right mindset

When making a custom image, _you are the distribution_. You have to think about what to include and what not to include in the image. You have to think about what files you can ship and what you can't.

This guide will use "you" to refer to the creator of the custom image, and "the user" to refer to its users. If you are making an image only for yourself, you are both parties, and can get away with more things.

## Resist the urge to add the entire universe

Systems like this are designed for a _small, lean, mean, maintainable, and performant core_. Remember that updates to the _base image_ require a reboot, so ideally you want that surface area to be small - let Flatpak and other userspace tools handle the rest. You can build a toolbox image that contains software and configuration not needed on the base image but useful to the image's user.

Also remember that these systems are atomic, you don't need to manually clean up an old decision, the user will just get a new pristine image (ideally every day), so if you need to add a bunch of packages to get the desired outcome then you can always trim it down later - just remember that you need to account for the user's data!

## What you can and cannot do

When making the image, you cannot do things that require a booted system, like creating user accounts and groups or writing to `/var/` where the user's files are stored. Instead, you should write to system directories like `/usr/bin/` and `/usr/etc/`, the proper place for default system configuration that is applied to the `/etc/` directory when the image is booted.

Some RPM packages might have issues because they try to create users or user groups, or write to the `/opt/` directory. The easiest workaround in these cases is to manually layer them on the booted image.