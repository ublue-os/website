# Installing Bazzite and Initial Setup

!!! WARNING
    Fedora's installer has some issues with OCI images currently since this feature is still new.  If you have any issues installing, please consult our FAQ page [here](/images/bazzite/FAQ/#i-am-having-issues-installing-bazzite-onto-my-hardware).

!!! ATTENTION

    Most of our ISOs require an internet connection! Make sure to connect to either a wired or wireless network inside the installer under the "Network" category to properly install it.

!!! ATTENTION

    It is **HIGHLY RECOMMENDED** to install Bazzite with a user password that has administrative privileges so you can install certain software.

This is a visual guide for installing Bazzite.

# Video Guides

<iframe width="560" height="315" src="https://www.youtube.com/embed/doQW1FyAISQ?si=2397_sSRIyC8fV5L" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/aaeRk8_i1Ds?si=GopDcKXcCUCxdie8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


## Pre-Requisites

* Make sure you meet the [system requirements](https://docs.fedoraproject.org/en-US/fedora/latest/release-notes/welcome/Hardware_Overview/) for Fedora Linux. 
* A graphics card that can utilize Vulkan 1.3 or later.  Most modern AMD, Nvidia, and Intel GPUs should be fine.
* The drive that Bazzite is installed to must have at least 32GB unallocated drive space.
* A USB flash drive, external drive, or microSD card with at least 5GB of free space on it. **(This will remove existing data on it!)**
* A working and stable wired or wireless internet connection.
* Download the latest ISO release [here](https://github.com/ublue-os/bazzite/releases).
* Software to flash the image to your flash drive, external drive, or microSD card.  We recommend using [Fedora Media Writer,](https://www.fedoraproject.org/en/workstation/download/) [Balena Etcher,](https://etcher.balena.io/) or [Rufus.](https://rufus.ie/en/) **Ventoy is unsupported.**
* Bazzite requires a physical wired keyboard to install properly.
* See [Fedora Kinoite documentation](https://docs.fedoraproject.org/en-US/fedora-kinoite/installation/) and [Fedora Silverblue documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) for more information.

## Boot into your installation medium.

Connect your bootable medium to your device and boot into it.  This depends on your hardware, most of the time it's the function keys (ex: <kbd>F9</kbd>).  It's very dependent on the motherboard in your device.  

Sometimes you need to consult the manual or read any hotkeys when you boot your PC.  You can alternatively change BIOS settings, which can also be any of the function keys, to boot with your flash drive first before your current storage, but this is not recommended to keep on after installing.

For the Steam Deck, hold the 'Volume Down' button and click the Power Button, and when you hear the chime, let go of the Volume Down button, and you'll be booted into the Boot Manager.  

When you get to the boot menu, select your bootable device to boot into the Bazzite installer.

## Bazzite Variants

When you boot into the installer, you will be presented a list of Bazzite images.

- Bazzite offers multiple images, but most images will be following **one of these two formats****: *Desktop* and *Steam Deck/HTPC*.  
       - *Desktop* images are for general desktop computing and attempt to mimic SteamOS's Desktop Mode in terms of functionality.  
       - *Steam Deck/HTPC* images boot directly into Game Mode and are intended for handheld PCs and home theater PCs.
- These images also come with the choice of [KDE Plasma](https://kde.org/plasma-desktop/) or [GNOME](https://www.gnome.org/) for their desktop environments.
   
### Common images:

![image](https://github.com/nicknamenamenick/website/assets/121328689/6ed9e4fd-0088-4f79-8f56-98b32ef3749b)


* **bazzite** is the AMD/Intel GPU general desktop image intended for most personal computers.

* **bazzite-nvidia** is _bazzite_ but for PCs running Nvidia GPUs as they include their proprietary drivers in the image.

* **bazzite-deck** is a special Steam Deck/HTPC/Handheld PC image of Bazzite.  More details on that [here.](https://github.com/ublue-os/bazzite#steam-deckhome-theater-pcs-htpcs)

* **bazzite-gnome** is _bazzite_, but instead of using KDE Plasma as the desktop environment, it uses GNOME.

* **bazzite-gnome-nvidia** is _bazzite-gnome_ but for PCs running Nvidia GPUs as they include their proprietary drivers in the image.

* **bazzite-deck-gnome** is _bazzite-deck_ but instead of using KDE Plasma as the desktop environment, it uses GNOME.

There are also images specific to specialized hardware like **bazzite-framework** (Framework hardware), **bazzite-surface** (Microsoft Surface hardware), etc.

## KDE Plasma and GNOME Desktop Environments Differences at a Glance

### KDE Plasma

![image](https://github.com/nicknamenamenick/website/assets/121328689/094fdb77-50d6-4705-81f7-b8cc6a049348)

- KDE Plasma's default interface has a traditional and familiar layout.
- Highly customizable.
- Uses Qt for GUI.
- Fedora Kinoite & SteamOS use KDE Plasma.

### GNOME

![image](https://github.com/ublue-os/website/assets/121328689/eac38977-404e-4363-9621-a801056c0135)


- GNOME's default interface has an elegant and touch-friendly layout.
- Workflow is designed to be out of the user's way.
- Uses GTK (GNOME Toolkit) for GUI.
- Fedora Silverblue & Ubuntu use GNOME.

## Installing Bazzite

After selecting the image the installation setup screen should come up:

![image](https://github.com/ublue-os/website/assets/121328689/04660187-1df7-4766-8b16-1a6ec9e35925)

* Select your language, region, keyboard layout, and time zone.
* Select your network. (**You need to be connected to internet for this to install properly!**)
* Select/Add the drive you would like to install Bazzite to.  (**This will delete all of the data on the drive!**)
* Make sure to only check the drive you plan to install Bazzite since all of your drives might be selected including microSD!
* Optionally encrypt the drive with a password if you wish.  (**If you lose this password, you will not be able to decrypt your drive!**)
* Setup a user account and **optionally** a root account, and begin the installation.

_Root account is mainly used on PCs with multiple users. You can give an **administrator password** to a single user account for root privileges._

Proceed with the installation.  This may take a long time to install and the progress indicator may not be accurate.

## First Boot Setup

After booting up for the first time after installation, a window will pop up saying "Welcome to Bazzite."  This is a utility that allows you to tailor Bazzite to your liking by configuring it and pre-installing applications.  It is necessary that you complete this step after installation.  

Click "Next" to begin configuring Bazzite.  Press the toggle switch button next to the item to have the option enabled or disabled for your installation, some are already toggled on by default.  If you want to adjust and customize any of the options, press the arrow next to the toggle switch button if available.

![image](https://github.com/ublue-os/website/assets/121328689/2aa3773d-4ab6-4520-abe2-fe7c98664e0b)

Login to Steam **(required for Steam Deck, HTPC, and Handheld PC images)**, and reboot your device when you finish.

If you have a microSD card and had game installed on SteamOS, and do NOT want to reinstall your video games, then select "Use EXT4 for SD cards" in the Bazzite Portal.

!!! NOTE

    For users with Secure Boot enabled: 
    Run `ujust enroll-secure-boot-key` in the host terminal and enter the password `ublue-os` if prompted to enroll the required key!

## Game on!

**You have installed Bazzite!**

If you need any additional applications check out the software center that comes preinstalled.  Look for the shopping bag icon called either Discover or GNOME Software depending on which variant of Bazzite you have installed.  Check out the most [popular software](https://flathub.org/apps/collection/popular/1) available to install.

## Linux Gaming Guide

For a quick run-through of the basics of gaming on desktop Linux, take a look [here](/images/bazzite/gaming_guide).

## Waydroid Setup

Check out the [Waydroid setup guide](/images/bazzite/waydroid) for Android support in Bazzite.

## Frequently Asked Questions

Check out the [Bazzite FAQ](/images/bazzite/FAQ).

<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM169.8 165.3c7.9-22.3 29.1-37.3 52.8-37.3h58.3c34.9 0 63.1 28.3 63.1 63.1c0 22.6-12.1 43.5-31.7 54.8L280 264.4c-.2 13-10.9 23.6-24 23.6c-13.3 0-24-10.7-24-24V250.5c0-8.6 4.6-16.5 12.1-20.8l44.3-25.4c4.7-2.7 7.6-7.7 7.6-13.1c0-8.4-6.8-15.1-15.1-15.1H222.6c-3.4 0-6.4 2.1-7.5 5.3l-.4 1.2c-4.4 12.5-18.2 19-30.6 14.6s-19-18.2-14.6-30.6l.4-1.2zM224 352a32 32 0 1 1 64 0 32 32 0 1 1 -64 0z"/></svg>](https://universal-blue.org/images/bazzite/FAQ/)
