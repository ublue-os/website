---
date: 2023-09-06
comments: true
authors: 
  - nicknamenamenick
links:
  - Bazzite Commits: https://github.com/ublue-os/bazzite/commits/main
---

# Bazzite Buzz No. 2

Bazzite has hit over 1,000 commits in a little over 200 days since the project's inception!  We now own the domains https://bazzite.gg and https://metrics.bazzite.gg for this project.  Offline ISOs are mostly ready to go, check it out below!

![](https://hackmd.io/_uploads/rkEiCkO6h.png)
<p style="text-align: center;">All hail the cube.</p>

Before we move on to the changes we've got a new installation video from [Justin Garrison](https://justingarrison.com/)

<iframe width="560" height="315" src="https://www.youtube.com/embed/doQW1FyAISQ?si=2397_sSRIyC8fV5L" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Features

## New ISOs

Thanks to [akdev1l](https://github.com/akdev1l/) we now have fresh offline ISOs available for testing! 

- [bazzite-38-x86_64.iso](https://ublue.download/bazzite-38-x86_64.iso) - [checksum](https://ublue.download/bazzite-38-x86_64.iso.CHECKSUM)
- [bazzite-deck-38-x86_64.iso](https://ublue.download/bazzite-deck-38-x86_64.iso) - [checksum](https://ublue.download/bazzite-deck-38-x86_64.iso.CHECKSUM)
- [bazzite-deck-gnome-38-x86_64.iso](https://ublue.download/bazzite-deck-gnome-38-x86_64.iso) - [checksum](https://ublue.download/bazzite-deck-gnome-38-x86_64.iso.CHECKSUM)
- [bazzite-gnome-38-x86_64.iso](https://ublue.download/bazzite-gnome-38-x86_64.iso) - [checksum](https://ublue.download/bazzite-gnome-38-x86_64.iso.CHECKSUM)
- [bazzite-gnome-nvidia-38-x86_64.iso](https://ublue.download/bazzite-gnome-nvidia-38-x86_64.iso) - [checksum](https://ublue.download/bazzite-gnome-nvidia-38.iso.CHECKSUM)
- [bazzite-nvidia-38-x86_64.iso](https://ublue.download/bazzite-nvidia-38-x86_64.iso) - [checksum](https://ublue.download/bazzite-nvidia-38-x86_64.iso.CHECKSUM)

## Features
- All images can now be signed through Bazzite Portal.
- Added calibrated color profiles for matte & reflective Steam Deck displays.
- Switch to using dedup service from [SteamOS-BTRFS](https://gitlab.com/popsulfr/steamos-btrfs).
- Added [ROM Properties](https://github.com/GerbilSoft/rom-properties). 
- Added [GModCEFCodecFix](https://github.com/solsticegamestudios/GModCEFCodecFix) for Garry's Mod to resolve launch issues on the Linux port.
- [Oversteer](https://github.com/berarma/oversteer) can now be installed in the Bazzite Portal.
- [Toolbox](https://github.com/containers/toolbox) is now restored.
- Chinese input now works properly.
- Changed the functionality of auto-start Big Picture Mode to auto-login on desktop images.
    - If you want the previous functionality back, enable "Start Steam in Big Picture Mode" in the Steam settings for previous behavior.
- Added twitter-twemoji-fonts, matching SteamOS.
- Nix package manager will now be added via the [Determinate Systems Nix Installer](https://github.com/DeterminateSystems/nix-installer).
- Nix packages are now automatically updated.
- [Fleek](https://github.com/ublue-os/fleek) is now an option for users using Nix.
- Upgraded [Greenlight](https://github.com/unknownskl/greenlight) to version 2.0.0.
- Added [PinApp](https://github.com/fabrialberio/PinApp) to Bazzite Portal under "Utilities."
- Memory Tuning option removed from Bazzite Portal on desktop images.
- Steam Deck images now mimic SteamOS's volume levels.
- Steam Deck images now uses the "flat" mouse acceleration profile to match SteamOS.
- Steam Deck images now use the native package of [Protontricks](https://github.com/Matoking/protontricks).
- GNOME images will now use [ProtonPlus](https://github.com/Vysp3r/ProtonPlus) over [ProtonUp-qt](https://github.com/DavidoTek/ProtonUp-Qt) by default.
- GNOME images will also ship the [AdwSteamGtk Flatpak](https://github.com/Foldex/AdwSteamGtk) for Steam.
- Automatic updates for [Firefox GNOME theme](https://github.com/rafaelmardojai/firefox-gnome-theme) and [Thunderbird GNOME theme](https://github.com/rafaelmardojai/thunderbird-gnome-theme).

# Fixes
- Updates are no longer triggered when checking for one on Steam Deck images. (Thanks [ChimeraOS](https://chimeraos.org/about/)!)
- Update progress bar's length is now longer and more granular on the Steam Deck images.
- Tons of Waydroid fixes.
- Tons of bazzite-arch distrobox container fixes.
- Max volume is now reduced to prevent overamplification.
- Fixed Steam reinstalling when switching to Game Mode.
- Fixed Steam reverting beta client selection in Game Mode.
- Fixed hardware detection in Bazzite Portal.
- Fixed non-steam-deck hardware being limited to 15W.
- Fixed updates not applying on Steam Deck images.
- Fixed typo in `just configure-waydroid`.
- Fixed auto-login in KDE images causing issues with the file picker.
- Fixed ibus errors in the KDE images.
- Fixed boot script slowdowns.
- Fixed Steam Deck images having issues with Night Mode and other color issues from this [PR](https://github.com/KyleGospo/gamescope/commit/27de6f3e5543c0ae725c70373de3e95d1e52fbff).
