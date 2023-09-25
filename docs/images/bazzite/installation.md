# Installing Bazzite and Initial Setup

This is a visual guide for installing Bazzite.

# Video Guides

<iframe width="560" height="315" src="https://www.youtube.com/embed/doQW1FyAISQ?si=2397_sSRIyC8fV5L" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/aaeRk8_i1Ds?si=GopDcKXcCUCxdie8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Installation tutorial begins at [1:37](https://youtu.be/aaeRk8_i1Ds?feature=shared&t=97).

## Pre-Requisites

* Make sure you meet the [system requirements](https://docs.fedoraproject.org/en-US/fedora/latest/release-notes/welcome/Hardware_Overview/) for Fedora.
* A graphics card that can utilize Vulkan 1.3 or later, but most modern AMD, Nvidia, and Intel GPUs should be fine.
* The drive that Bazzite is installed to must have at least 20GB unallocated drive space.
* A USB flash drive, external drive, or microSD card with at least 3GB of free space on it. **(Keep in mind this will remove existing data on it!)**
* A working, stable, wired or wireless internet connection.
* Download an ISO release [here.](https://github.com/ublue-os/bazzite/releases)
* Software to flash the image to your flash drive or external drive.  We recommend using [Fedora Media Writer,](https://www.fedoraproject.org/en/workstation/download/) [Balena Etcher,](https://etcher.balena.io/) or [Rufus.](https://rufus.ie/en/) **Ventoy is unsupported.**
* Bazzite requires a physical keyboard to install properly on a Steam Deck.
* Manual partitioning is unsupported.
* See [Fedora Kinoite documentation](https://docs.fedoraproject.org/en-US/fedora-kinoite/installation/) and [Fedora Silverblue documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) for more information.


## Bazzite Variants
- Bazzite offers multiple images, but most images will be following one of these **two** formats: *Desktop* and *Steam Deck/HTPC*.  
  - *Desktop* images are meant for general desktop computing and attempt to mimic SteamOS's Desktop Mode in terms of functionality.  
  - *Steam Deck/HTPC* images boot directly into Game Mode and are intended for handheld PCs and home theater PCs.
- These images also come with the choice of KDE Plasma or GNOME as - the desktop environment.
   
### Common images:
![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/6d52a35b-ec89-4180-8940-173ce37a6200)

* **bazzite** is the AMD/Intel GPU general desktop image intended for most personal computers.

* **bazzite-nvidia** is _bazzite_ but for PCs running Nvidia GPUs as they include their proprietary drivers in the image.

* **bazzite-deck** is a special Steam Deck image of Bazzite.  More details on that [here.](https://github.com/ublue-os/bazzite#steam-deckhome-theater-pcs-htpcs)

* **bazzite-gnome** is _bazzite_, but instead of using [KDE Plasma](https://kde.org/plasma-desktop/) as the desktop environment, it uses [GNOME.](https://www.gnome.org/)

* **bazzite-gnome-nvidia** is _bazzite-gnome_ but for PCs running Nvidia GPUs as they include their proprietary drivers in the image.

* **bazzite-deck-gnome** is _bazzite-deck_ but instead of using [KDE Plasma](https://kde.org/plasma-desktop/) as the desktop environment, it uses [GNOME.](https://www.gnome.org/)

There are also images specific to specialized hardware like **bazzite-framework**, **bazzite-surface**, etc. 

## KDE Plasma and GNOME Desktop Environments Differences at a Glance

### KDE Plasma

![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/afd257bd-1a66-48d2-980c-dc7ef6614d47)

### GNOME

![image](https://github.com/nicknamenamenick/bazzite/assets/121328689/0a4ff5fe-322d-4806-b13e-7f7081d48ca0)

## Installing Bazzite

You will be presented with an installation screen.  

* Select your language, region, keyboard layout, and time zone.
* Select your network. (**You need to be connected to internet for this to install properly!**)
* Select/Add the drive you would like to install Bazzite to.  (**This will delete all of the data on the drive!**)
* Optionally encrypt the drive with a password if you wish.  (**If you lose this password, you will not be able to decrypt your drive!**)
* Setup a user account and **optionally** a root account, and begin the installation.

_Root account is mainly used on PCs with multiple users. You can give an administrator password to a single user for root privileges._

## Wayland and X11

In short, Wayland and X11 (also known as Xorg or the X Window System) are windowing systems for desktop Linux.

* Wayland is the default for most of the images and the recommended option for Bazzite.
* X11 is a legacy windowing system. While we recommend to stick with Wayland, there may be scenarios where X11 would have to be used. Nvidia GPUs may have issues with Wayland.

## First Boot Setup

After logging in for the first time after installation a window will pop up saying "Welcome to Bazzite."  This is a utility that allows you to tailor Bazzite to your liking by configuring and pre-installing applications.  

Click "Next" to begin configuring Bazzite.  Press the toggle switch button next to the item to have the option enabled or disabled for your installation, some are already toggled on by default.  If you want to adjust and customize any of the options, press the arrow next to the toggle switch button if available.

![image](https://github.com/ublue-os/website/assets/121328689/2aa3773d-4ab6-4520-abe2-fe7c98664e0b)

Reboot your device when you finish.

## Game on!

You have installed Bazzite!  

If you need any additional applications check out the software center that comes preinstalled.  Look for the shopping bag icon called either Discover or GNOME Software depending on which variant of Bazzite you have installed. If you wish to see what software is in the store before installing, or when you're off of your device, click [here.](https://flathub.org/apps/collection/popular/1)

## Linux Gaming Guide

For a quick run-through of the basics of gaming on desktop Linux, take a look [here](/images/bazzite/gaming_guide).

## Waydroid

Check out the Waydroid guide [here](/images/bazzite/waydroid).

## Frequently Asked Questions

Link to that [here](/images/bazzite/FAQ).
