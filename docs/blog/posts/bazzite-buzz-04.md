---
date: 2023-09-28
comments: true
authors: 
  - nicknamenamenick
links:
  - Bazzite Commits: https://github.com/ublue-os/bazzite/commits/main
  - Bazzite 1.0: https://universal-blue.org/blog/2023/08/20/bazzite-10/
---
# Bazzite Buzz No. 4

![](https://hackmd.io/_uploads/rJy2vAjka.jpg)

<p style="color: blue"> Welcome to Bazzite Buzz #4!</p> 

Bazzite is a custom image of Fedora 38 designed to being the best in Linux gaming to your PCs, including the Steam Deck. This newsletter highlights all the work we are doing to bring gamers the best goodies for their PCs and handheld gaming devices.

If you are new to a Universal Blue project then here's some back filler: These images follow the [continuous delivery](https://continuousdelivery.com/) methodology of development. That means we're constantly adding new things, so let's get started!

Today we have released a new batch of online ISOs.  Our offline ISOs that we had released earlier had some issues with the Steam Deck's resolution, but eventually this will all be sorted out. When that happens we will release a new batch of offline ISOs in the future.  In the meantime, grab the latest online ISO and **make sure to connect to the internet in the installer.**

    
Initial work has been done to have Bazzite boot on the Asus ROG Ally handheld PC!  If you are interested in testing and trying it out then download [Fedora Kinoite](https://fedoraproject.org/kinoite/download/) and install it like you normally would Bazzite.  Follow our installation instructions [here](https://universal-blue.org/images/bazzite/installation/).  Once you reach the desktop, open Konsole and enter either:
`rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-ally:latest` for KDE Plasma or `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-ally-gnome:latest` 
for GNOME. You are now rebasing to the ally image.  After it has finished rebasing then reboot the device.  Be aware that it may have issues, but please report them on our [Github Issue Tracker](https://github.com/ublue-os/bazzite/issues).
    
We also now support Framework, Lenovo Legion, and ASUS devices with their own special images.  Generic controller support for handheld PCs with our addition of `hanygccs`.  In addition, Tailscale now has support out of the box and the GNOME images include the Tailscale status extension too.  Fleek is temporary removed until non-interactive installer is finished.  KDE images can now share their screen properly on Wayland with the inclusion of xwaylandbridge.  We also added `android-udev-rules` to the base image and a `just` command to add scrcpy.  This can also give you access to [guiscrcpy](https://guiscrcpy.srev.in/) to mirror your Android phone.

![](https://hackmd.io/_uploads/SyQMrBCkp.png)

<p style="text-align: center;font-weight: bold">Here is guiscrcpy mirroring an Android phone.</p>

![](https://hackmd.io/_uploads/ry4U7bpk6.png)
<p style="text-align: center;font-weight: bold">Adwaita Steam skin using Decky's CSS Loader plugin on a desktop Bazzite image.</p>
<p style="text-align: center; font-weight: 600; color: green">(Yes it works on KDE Plasma too.) </p>

We'd like to thank all of our contributors and those who are helping us troubleshoot any issues in our newer builds.



# New Features
- Added support for Framework devices.
- Added support for ASUS devices.
- Added support for Lenovo Legion devices.
- Added nct6687 driver for `lm_sensors` since it is needed on certain AMD B550 motherboards.
- Added [handygccs](https://github.com/ShadowBlip/HandyGCCS) for handheld PCs.
- Added [Tailscale](https://github.com/tailscale/tailscale) support out of the box.
- Added [Linux Mint's](https://linuxmint.com/) [Web App Manager](https://github.com/linuxmint/webapp-manager) application.
- Added Waydroid utilities.
- Added [Solaar](https://github.com/pwr-Solaar/Solaar) and [Resilio Sync](https://www.resilio.com/individuals/) to Bazzite Portal.
- Oversteer is now added via udev rules so it does not have to be layered. 
- Removed AdwSteamGtk since it is recommended to install this theme via the [CSS Loader](https://github.com/suchmememanyskill/SDH-CssLoader) Decky plugin.
- `vm.max_map_count` increased to match SteamOS.
- Signing is now removed from Bazzite Portal since it now automatic.
- Nvidia images now has a helpful message about secure boot.
- GNOME images now play a sound when the battery is low.
- GNOME images now include the [gamerzilla-shell-extension](https://github.com/dulsi/gamerzilla-shell-extension)
- GNOME images now include the Tailscale status GNOME shell extension. 
- Steam Deck images will now build Steam RPM to avoid RPM Fusion dependency issues.
- KDE color control is now added except for Nvidia images.
- Corrected issue with Garry's Mod's `just` command.
- Standardized nomenclature for `just` commands concerning game fixes.
- Added a `just` command for installing Adwaita-for-Steam, will be automatically updated.
- Added a `just` command to fix SteamVR on desktop images.
- Added a `just` command to completely remove and reset bazzite-arch.
- Added a `just` command [xwaylandbridge](https://github.com/KDE/xwaylandvideobridge) for KDE Plasma images.  This fixes screensharing issues.
- Added a `just` command to add [scrcpy](https://github.com/Genymobile/scrcpy).

# Fixes
- Fixed numerous issues with Steam.
- Fixed numerous issues with Distrobox containers
- Fixed hide/unhide GRUB `just` command.
- Use current GRUB paths.
- Added default-enabled option to disable TDP and other hardware controls on non-deck hardware.  This should fix TDP issues on other devices.
- Moved extest back on desktop images and is optional to use. 
- Fixed Steam Deck images having a broken "Return to Game Mode" shortcut if they had desktop auto-login enabled.
- Fixed `bazzite-hardware-setup` executing every boot.
- Fixed other auto-login issues on all images.
- Adjustments to the `bazzite-arch` container.
-  Fixed justfile creation.  Currently, this only gets written if the file exists. Create it when the file doesn't exist instead.
-  Reorganized `just` commands.
-  Lutris dependency for PCEM is now added.


Full changelog and ISOs for the 1.2.0 release [here](https://github.com/ublue-os/bazzite/releases/tag/v1.2.0).
