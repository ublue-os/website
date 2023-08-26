---
date: 2023-08-26
comments: true
authors: 
  - nicknamenick
  - castrojo
---

# Bazzite Buzz No. 1

Bazite 1.0 released last week, but the hum of progress continues! 

If you are new to a Universal Blue project here's some back filler: These images follow the [continuous delivery](https://continuousdelivery.com/) methodology of development. 

We build on top of the Fedora base and then build our customizations on top every day and on every change. That means when we fix something or add a new feature everyone gets it. So if we fix one of your issues it can be in your device in less than 15 minutes, and usually faster. Neat. The more people help out, the greater the pace of features and goodies.

In order to help with that we'll start publishing these Bazzite notes regularly so you can keep pace with what's happening. Here's a great tour video from Hi-Tech Lo-Life showing off some Bazzite features.

<iframe width="560" height="315" src="https://www.youtube.com/embed/aaeRk8_i1Ds" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<br/>
<br/>

## Features

- Added [Gear Lever](https://github.com/mijorus/gearlever) to manage AppImages.
- Added equalizer settings for mic from SteamOS
- Added NTP by default to fix inaccurate clock information like the time & date.
- Added Valve's audio firmware from SteamOS.
- Added [wmctrl](https://www.freedesktop.org/wiki/Software/wmctrl/), useful for resizing windows in Game Mode.
- Ignore microphones on headsets with microphones from SteamOS.
- Added loopback audio sources.
- Neofetch is now replaced with [Hyfetch](https://github.com/hykilpikonna/hyfetch) by default. (Neofetch is still available however.)
- For GNOME variants: Added [Hanabi](https://github.com/jeffshee/gnome-ext-hanabi) for videos as desktop wallpapers.
- Added new features and fixed issues with GNOME variants of Bazzite.
    - Removed unnecessary preinstalled applications.
    - Added [Extension Manager](https://flathub.org/apps/com.mattjakeman.ExtensionManager) to replace Extensions.
    - Fixed VRR not working.
    - Removed AppIndicator as a preinstalled extension.

## Fixes
- Preserve Decky launcher after updates.
- Decky now uses the "release" branch as opposed to "pre-release" by default.
- Added missing dependency for Lutris.
- Added missing dependency to SteamTinkerLauncher.
- Major Distrobox cleanup for a more stable experience.
- Fixed battery limit service to match SteamOS.
- Fixed fish shell not working system-wide.
- Fixed Bazzite Portal not installing certain things and relaunching at every boot.
- Multiple fixes to Waydroid.
- The Steam Deck variant defaults to X11 in Desktop Mode by default to resolve issues.  Wayland is still an option.
