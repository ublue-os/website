# Installing Bazzite and Initial Setup

This guide is a visual guide for those who are unfamiliar with desktop Linux and want to install Bazzite.

# Prerequisites:
* Make sure you meet the [system requirements](https://docs.fedoraproject.org/en-US/fedora/latest/release-notes/welcome/Hardware_Overview/) for Fedora.
* A graphics card that can utilize Vulkan 1.3 or later, but most modern AMD, Nvidia, and Intel GPUs should be fine.
* A USB flash drive, external drive, or microSD card with at least 3GB of free space on it. **(Keep in mind this will remove existing data on it!)**
* Download an ISO release [here.](https://github.com/ublue-os/bazzite/releases)
* Software to flash the image to your flash drive or external drive.  We recommend using [Fedora Media Writer,](https://www.fedoraproject.org/en/workstation/download/) [Balena Etcher,](https://etcher.balena.io/) or [Rufus.](https://rufus.ie/en/)
* Manual partitioning is unsupported.
* See [Fedora Kinoite documentation](https://docs.fedoraproject.org/en-US/fedora-kinoite/installation/) and [Fedora Silverblue documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) for more information.


# Bazzite Variants

![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/6d52a35b-ec89-4180-8940-173ce37a6200)
* **bazzite** is the AMD/Intel GPU general desktop image intended for most personal computers.
* **bazzite-nvidia** is _bazzite_ but for PCs running Nvidia GPUs as they include their proprietary drivers in the image.
* **bazzite-deck** is a special Steam Deck image of Bazzite.  More details on that [here.](https://github.com/ublue-os/bazzite#steam-deck)
* **bazzite-gnome** is bazzite, but instead of using [KDE Plasma](https://kde.org/plasma-desktop/) as the desktop environment, it uses [GNOME.](https://www.gnome.org/)
* **bazzite-gnome-nvidia** is _bazzite-gnome_ but for PCs running Nvidia GPUs as they include their proprietary drivers in the image.
* **bazzite-deck-gnome** is _bazzite-deck_ but instead of using [KDE Plasma](https://kde.org/plasma-desktop/) as the desktop environment, it uses [GNOME.](https://www.gnome.org/)


## KDE Plasma and GNOME Desktop Environments Differences at a Glance

### KDE Plasma:

![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/afd257bd-1a66-48d2-980c-dc7ef6614d47)

### GNOME:

![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/0a4ff5fe-322d-4806-b13e-7f7081d48ca0)

# Installing Bazzite

You will be presented with an installation screen.  

* Select your language, region, keyboard layout, and time zone.
* Select your network. (**You need to be connected to internet for this to install properly!**)
* Select/Add the drive you would like to install Bazzite to.  (**This will delete all of the data on the drive!**)
* Optionally encrypt the drive with a password if you wish.  (**If you lose this password, you will not be able to decrypt your drive!**)
* Setup a user account and **optionally** a root account, and begin the installation.

_Root account is mainly used on PCs with multiple users.  You can give an administartor password to a single user for root privileges._

# Wayland and X11

![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/ec5d1134-721e-4a4d-bf51-43f12ffc4043)

In short, Wayland and X11 (also known as Xorg or the X Window System) are windowing systems for desktop Linux.

* Wayland is the default for most of the images and the recommended option for Bazzite.  However, the Nvidia images default to X11.
* X11 is a legacy windowing system.  While we recommend to stick with Wayland, there may be scenarios where X11 would have to be used.  Nvidia GPUs may have issues with Wayland.

## First Boot Setup

After logging in for the first time after installation a window will pop up saying "Welcome to Bazzite."  This is a utility that allows you to tailor Bazzite to your liking by configuring and preinstalling applications.  

Click "Next" to begin configuring Bazzite.  Press the toggle switch button next to the item to have the option enabled or disabled for your installation, some are already toggled on by default.  If you want to adjust and customize any of the options, press the arrow next to the toggle switch button if available.

![image](https://github.com/ublue-os/website/assets/121328689/2aa3773d-4ab6-4520-abe2-fe7c98664e0b)

Reboot your device when you finish.

## Game on!

Congratulations! You have installed Bazzite!  

If you need any additional applications check out the software center that comes preinstalled.  Look for the shopping bag icon called either Discover or GNOME Software depending on which variant of Bazzite you have installed. If you wish to see what software is on here before installing or when you're off of your device, click [here.](https://flathub.org/apps/collection/popular/1)

## Gaming Tips and Tricks

For a quick runthrough of the basics of gaming on desktop Linux take a look [here.](https://github.com/ublue-os/website/new/main/docs/images/bazzite/gaming_guide.md)

## Waydroid

If you wish to use Waydroid, a setup guide can be found [here](/images/bazzite/waydroid).
