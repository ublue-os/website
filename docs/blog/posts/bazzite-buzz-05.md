---
date: 2023-10-04
comments: true
authors: 
  - nicknamenamenick
links:
  - Bazzite Commits: https://github.com/ublue-os/bazzite/commits/main
  - Bazzite 1.0: https://universal-blue.org/blog/2023/08/20/bazzite-10/
---
![](https://hackmd.io/_uploads/ryvAQvC16.jpg)
<hr>

<p style="text-align: center; font-weight: 600; color: red">IMPORTANT: MANUAL INTERVENTION REQUIRED</p>

If you installed a Bazzite image on any device **before September 22, 2023** or used the **older offline ISO** then open a host terminal and enter `rpm-ostree update`, and wait for it to upgrade to the latest build.  Reboot your device after it has finished.  More information on this [here](https://github.com/ublue-os/bazzite/issues/382).
<hr>

<p style="font-weight:900; font-size: 25px">Welcome to Bazzite Buzz #5!</p>

Bazzite is a custom image of Fedora 38 designed to being the best in Linux gaming to your PCs, including the Steam Deck. This newsletter highlights all the work we have been doing to bring gamers the best goodies for their PCs and handheld gaming devices.

If you are new to a Universal Blue project then here's how they work then here's how they work. They follow the [continuous delivery](https://continuousdelivery.com/) methodology of development. That means we're constantly adding new things, so let's get started!

We have been preparing for the stable release of Fedora 38 and will plan to switch builds over there within the next two weeks.  Nvidia images for ASUS and Microsoft Surface hardware is now available.  We also added dependencies needed for the [DaVinci Resolve](https://www.blackmagicdesign.com/products/davinciresolve) video editor in case you wanted that.  The [`unrar`](https://github.com/aawc/unrar) library is included in the image which should resolve issues users may experience with certain compressed file formats.

![](https://hackmd.io/_uploads/HJ7I-9jlp.png)

<p style="text-align: left;font-weight: bold;font-size: 12px">Bazzite Portal has new additions</p>


Bazzite Portal now features more software including the [Brew package manager](https://github.com/Homebrew/brew), [OpenTabletDriver](https://github.com/OpenTabletDriver/OpenTabletDriver), and [Wootility](https://wootility.io/).  It also features the unofficial [Final Fantasy XIV launcher](https://github.com/goatcorp/FFXIVQuickLauncher) since it works better on Linux.

Steam Deck images now include a ton of performance optimizations taken from this [Medium article](https://medium.com/@a.b.t./here-are-some-possibly-useful-tweaks-for-steamos-on-the-steam-deck-fcb6b571b577).  These tweaks in theory should give a slight performance increase versus stock SteamOS, but we never attempted benchmarks yet to actually confirm this.  Maybe for a later time unless someone out there wants to volunteer and [benchmark](https://github.com/flightlessmango/MangoHud#fps-logging) both operating systems themself.

Waydroid support has also been both streamlined and improved tremendously.  Controllers, including the Steam Deck's contorls, should work well with it now.  Steam Deck images should have a working quick access menu with it and plus the addition of the framerate limiter working with Android applications to our surprise.

![](https://hackmd.io/_uploads/BJV4J75l6.png)

<p style="text-align: left;font-weight: bold;font-size: 12px">Waydroid on the Steam Deck running in Game Mode</p>

Open a host terminal and enter `just init-waydroid` and it should setup Waydroid for you.  Keep in mind you may need to set SELinux to permissive, but there has been conflicting reports on this.  If you are experiencing issues then enter `sudo nano /etc/selinux/config` and changing `SELINUX=enforcing` to `SELINUX=permissive`.  If you want extra goodies to Waydroid like ARM translation then enter `just configure-waydroid`.

We are now focusing on having an extremely stable and consistent experience across different hardware.  We are also planning on proper support for the ASUS ROG Ally and other handheld PCs, and have already accomplished some of the ground work necessary.  We still urge that both the ROG Ally and other handheld PCs are still only in the testing  phase at this moment, and users will encounter major issues until they are resolved.

As always, we'd like to thank all of our contributors and those who are helping us troubleshoot any issues in our newer builds.  The next Bazzite Buzz will focus on the transition from Fedora 38 to Fedora 39, so stay tuned for that.

New users who want to give Bazzite a try, here is the the latest [**online ISO**](https://github.com/ublue-os/bazzite/releases/tag/v1.2.0). Check out the [installation guide](https://universal-blue.org/images/bazzite/installation/) and [FAQ](https://universal-blue.org/images/bazzite/FAQ/), and if you experience any issues then please refer to our [issue tracker](https://github.com/ublue-os/bazzite/issues) and create one if your issue is not here.


# Features
- Nvidia support for ASUS and Microsoft Surface images.
- Streamlined Waydroid by adding [Weston launcher](https://wiki.archlinux.org/title/Weston) using polkit to start and stop the service. 
- Added controller support to Waydroid.
- The frame limiter in Game Mode now works for Android games in Waydroid.
- Added dependencies required by [DaVinci Resolve](https://www.blackmagicdesign.com/products/davinciresolve)
- Added the [`unrar`](https://github.com/aawc/unrar) library.
- Added [Brew package manager](https://github.com/Homebrew/brew) to Bazzite Portal
    - If you opt to use Brew, it will also auto-update those packages as needed.
- [OpenTabletDriver](https://github.com/OpenTabletDriver/OpenTabletDriver) has been added to Bazzite Portal
- Added [XIV Launcher](https://github.com/goatcorp/FFXIVQuickLauncher) to Bazzite Portal.
- Added option to download [Wootility](https://wootility.io/) to Bazzite Portal.
- Added option to force Discover Overlay to launch on GNOME Wayland.
- Added a `just` command to enable virtualization and vfio for desktop images.
- Upgraded Discover Overlay to version 0.6.9
- Upgraded Greenlight to 2.0.0-beta14 in Bazzite Portal.  Keep in mind Gear Lever constantly allows this and other AppImages to get updated post-installation.
- Advanced users can change Flatpak files if desired now since they moved from `/usr/etc` to `/etc/`.
- Updated Mesa to version 23.2.1.
- Updated boot menu for new images and simplified it.
- Waydroid now has the required properties for Steam Deck images.  No need to add `ro.sf.lcd_density=215` manually.
- Steam Deck images have a longer progress bar length.
- A few **preliminary** ASUS ROG Ally additions.
- Steam Deck images now use [`steam-patch`](https://github.com/Maclay74/steam-patch) which is especially useful for the ASUS ROG Ally and other handheld PCs.
    - Enabled TDP control on non-deck hardware covered by steam-patch too.
- Steam Deck images are now using some of the peformance tweaks from this [Medium article](https://medium.com/@a.b.t./here-are-some-possibly-useful-tweaks-for-steamos-on-the-steam-deck-fcb6b571b577).
    - Kyber I/O scheduling from BFQ
    - Disable `watchdog`
    - Raise `memlock` limit
        - Fedora already includes the 1000hz tick for the kernel & MGLRU. 
        - Once Valve solves their issue with CPPC in the Steam deck's firmware the Bazzite can also utilize `amd-pstate` to save on battery.


# Fixes
- Fixed handygccs not working on other hardware outside of the Steam Deck.
- Fixed Steam not opening after entering sleep mode.
- Corrected issue with updater run from systemd.
- Call daemon-reload when installing OpenTabletDriver & Resilio Sync.
- Correct typo that caused issues in Bazzite Portal. 
- Fixed Nvidia images losing kernel arguments by having them checked on every boot.
- If hostname is too long for Distrobox to function properly, it will reset to "bazzite".


Full changelog [here](https://github.com/ublue-os/bazzite/pull/379).

[<svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/)
