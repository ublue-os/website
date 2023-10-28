---
date: 2023-10-27
comments: true
authors: 
  - nicknamenamenick
categories:
  - bazzite
links:
  - Bazzite Commits: https://github.com/ublue-os/bazzite/commits/main
  - Bazzite 1.0: https://universal-blue.org/blog/2023/08/20/bazzite-10/
---
# Bazzite Buzz #6: Bazzite Rebrand

![image](https://github.com/ublue-os/website/assets/121328689/730de727-6ecc-4e77-af65-e47ed4af497e)

### Happy Early Halloween! 🎃

It has been a while since our last newsletter, and this was intended to be published with the release of Fedora 39.  Fedora 39 builds were intended to release originally on October 24th.  Fedora 39 was delayed until October 31st, and now it lands on November 7th after another delay unless the blockers get resolved before.  However, you can test and preview the Fedora 39 builds of Bazzite right now.  Instructions on that later on. This post has to cover a ton of new features that came out since the last newsletter, so let's get started!

Bazzite is a custom image of [**Fedora 38** (and eventually 39)](https://www.fedoraproject.org/) utilizing Universal Blue's custom image framework designed to bring users the best in Linux gaming for their PCs, including the Steam Deck. This newsletter highlights all of the work we have been doing to bring gamers the best features ready to go for their PCs, home theater setups, and handheld gaming devices.

If you are new to the project then here's how it works.  They follow the [continuous delivery](https://continuousdelivery.com/) methodology of development which means we're constantly adding new features and squashing bugs to the image through updates. These updates also include any updates directly from upstream from Fedora or upgrades from [packages](https://github.com/ublue-os/bazzite#custom-packages) we include.

This newsletter's highlight is all about the rebranding that Bazzite has undergone a couple of weeks ago.  This new branding has affected not only the documentation, but also appears throughout all of the images.

## Rebranding

![image](https://github.com/ublue-os/website/assets/121328689/368333ff-e260-4770-877d-99a010331eb3)

![image](https://github.com/ublue-os/website/assets/121328689/27f6c942-990e-420f-8977-ed17e070043a)

Bazzite has rebranded thanks to the design work of [rei0260](https://discord.com/users/rei0260). This new branding will also appear in Bazzite now by default.  Previously, the project only displayed the Fedora and SteamOS branding, but now the project has a standalone identity.  There are also new user avatars based on Valve games for both KDE and GNOME images of Bazzite.  You can change to any of these in the settings.

<img 
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 30%;"
    src="https://github.com/ublue-os/website/assets/121328689/d2d4927e-b66f-4611-9bd1-48df045b485e">
</img>
<img
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 45%;"
    src="https://github.com/ublue-os/website/assets/121328689/f052aa47-4bc6-4d6e-b173-3ecfbd6093fc">
</img>

<p style="text-align: center;font-weight: bold;font-size: 16">New Valve themed avatars for KDE & GNOME user avatars. </p>

## Nvidia Rework, OBS-VKCapture, and Other New Additions

Nvidia images have now been reworked to  Steam, Lutris vkBasalt, MangoHUD, Vulkan-Tools, and LatencyFlex as part of the image as opposed to using the `bazzite-arch` Distrobox container like the AMD/Intel images.  This was due to issues with Nvidia 32-bit libraries in the container, and it was just simpler to have these packages as part of the host.  We would prefer not to have these packages on the host like this, but dealing with Nvidia's proprietary driver erratic behavior has made this the best solution for now.

<p style="text-align: center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/gcKpCFQMzr4" title="Crysis on Deck (Captured on Bazzite with OBS &amp; OBS-VKCapture)" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></p>

<p style="text-align: center;font-weight: bold;font-size: 11px">A stress test of Crysis recorded with OBS-VKCapture with hardware encoding (VA-API H.264) on a Steam Deck in Game Mode.</p>

[OBS-VKCapture](https://github.com/nowrep/obs-vkcapture) is now added to easily record videos using hardware acceleration.  This also works in Game Mode meaning you can record your games without the use of a capture card.  If you are interested in trying this out in Game Mode, then open the game properties for the game you want to record and enter `OBS_VKCAPTURE=1 %command%` in the launch options.

![image](https://github.com/ublue-os/website/assets/121328689/f99acba7-0186-48c3-891c-4d61bf95eeb8)
<p style="text-align: left;font-weight: bold;font-size: 12px">Example of a GNOME desktop nested inside of a GNOME desktop.</p>

Other new features like the ability for your Steam Deck, handheld PC, or HTPC to have nested desktops.  Now you can run Desktop Mode inside of Game Mode without the inconvenience of switching between the two. Unfortunately, GNOME images cannot run applications in this nested desktop currently, but KDE images work fine right now.  Also, these Game Mode centric images can turn off the screen when the device shuts off through [libCEC](https://libcec.pulse-eight.com/) with compatible devices and HDMI cables. Windows files will now display metadata information for the appropriate files.  For example, Windows executables that have an icon will now display that icon in the file manager.

## Media Coverage & Translations

Bazzite and Universal Blue have been showcased by a ton of different [Youtube content creators and news publications](https://universal-blue.org/media/).  Most of these videos and articles are in English, but here is a showcase of Bazzite by a popular Brazilian Linux content creator:

<p style="text-align:center;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/qQ8uoBQIZ1I" title="Fizeram um novo sistema operacional para Gamers" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> </p>

Translations to Bazzite's [documentation](https://github.com/ublue-os/website/tree/main/docs/images/bazzite) in different languages would be appreciated! The Linux desktop is used internationally, and it would be great for the Bazzite documentation to reflect that.  If anyone would like to make translations for the project, then please feel free to contribute.  Bazzite already has multiple language support due to Fedora already providing that for us, but our documentation is only avaliable in English currently.

While we're on the topic of media coverage, special thanks to everyone who has made a video or written an article about Bazzite.  We are humbled by all of the support from our community and are grateful for those promoting the project.

## Closing Thoughts, Fedora 39 Testing, Bluefin, and Survey

We are nearing the 2.0 release of Bazzite.  It has been both a bumpy yet exciting ride few months releasing Bazzite out into the wild.  Our goal is to have Bazzite remain a very stable and consistent experience across different hardware and configurations when the Fedora 39 builds are out.  We had fixed edge-case scenarios and issues that had gone overlooked for the last three months.  However, one of the major issues that has plagued Bazzite since we released ISOs is Fedora's installer not cooperating with our OCI image method.  Please check our [FAQ](https://universal-blue.org/images/bazzite/FAQ/#i-am-having-issues-installing-bazzite-onto-my-hardware) if you have issues installing Bazzite.

Fedora 39 can be tested right now by rebasing to the 39 builds.  These Bazzite builds are considered "Release Candidate (RC)" right now, but there will be missing packages since many repositories do not build for unstable versions of Fedora.  If you want to test it now, open a host terminal and enter the command based on the image you're using.  Here are some examples:

`rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite:39` for the AMD/Intel Desktop image

`rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck:39` for the Steam Deck / HTPC image.

Refer to the Universal Blue [full image list](https://universal-blue.org/images/#latest) and replace `:latest` with `:39` for the image you're currently on to upgrade to the Fedora 39 builds right now.  **Please note:** Once you rebase to the 39 testing builds, you will have to rebase back to `:latest` once Fedora 39 is out.    When Fedora 39 has a stable release, then it will be upgraded for everyone in an update.

For those waiting on ASUS ROG Ally support, a lot of work has been done these past weeks to get it working properly.  The current state of Bazzite on the Ally is that it's slowly working.  We are hoping to resolve this in the coming months, but for those curious, the `bazzite-ally` does boot with major controller issues right now.  If you would like to help debug Bazzite on the ASUS ROG Ally, or other unique handheld hardware, then get in touch with us.  There are already trackers for [other handheld hardware](https://github.com/ublue-os/bazzite/issues/468) right now. We would like to thank everyone who has been helping us with proper support for all of the other handheld devices on the market.

We would like to thank our community for helping the project grow into what it is today.  Universal Blue has [announced](https://www.ypsidanger.com/announcing-project-bluefin/) a new image coming to beta soon known as [Bluefin](https://projectbluefin.io/).  It is a Fedora Linux image which is a curated GNOME experience that has the reliability of ChromeOS, but with the power of the modern Linux desktop.  Bazzite is the more gaming focused between the two, but Bluefin offers the [`bazzite-arch`](https://github.com/ublue-os/bazzite-arch) Distrobox container which is utilized in the Bazzite desktop images.  Bluefin also allows developers to have access to many of the standard tools and container-focused work environments with a single command. Give it a try sometime, and this is a reminder that [anyone can make their own custom image for Fedora](https://universal-blue.org/guide/fork-your-own/).

New users who want to give Bazzite a try, here is the the [**latest releases**](https://github.com/ublue-os/bazzite/releases). Check out the [installation guide](https://universal-blue.org/images/bazzite/installation/) and [FAQ](https://universal-blue.org/images/bazzite/FAQ/), and if you experience any issues, then please refer to our [issue tracker](https://github.com/ublue-os/bazzite/issues).  Also, discuss any feature requests or questions you have about Bazzite [here](https://github.com/orgs/ublue-os/discussions/categories/bazzite).

Lastly, we have a [**survey**](https://opnform.com/forms/your-bazzite-experience-sohzei) out now that we encourage you to fill out for feedback on the project.  We also want to gather statistics on what hardware that Bazzite is being installed on.  Thank you in advance if you participate in it.  This should only take about 5 minutes to complete.

<img 
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 30%;"
    src=https://hackmd.io/_uploads/BySgqkWMa.gif
    alt="Bazzite GIF">
<p style="text-align: center;font-weight: bold;font-size: 12px"> Rebranding GIF by Gecked.</p>


## Changelog👻

### New Features
- Branding has been updated!
    - New neofetch logo.
    - New boot logo.
    - New Bazzite Portal logo.
    - New logo appears throughout in both KDE Plasma and GNOME images.
    - New user avatars based on Valve games.
- Nvidia images have now switched Steam from Distrobox container to having these packages apart of the image to avoid issues with 32-bit libraries.
    - This change also means we removed the `bazzite-arch` distrobox container from Nvidia images.
    - Lutris, LatencyFlex, vkBasalt, MangoHUD, and Vulkan-Tools are also now part of the image.
- Switch to new [obs-vkcapture](https://github.com/nowrep/obs-vkcapture) package.
- Added CEC control to all images. (Thanks to [BoukeHaarsma23](https://github.com/BoukeHaarsma23/) and [ChimeraOS!](https://chimeraos.org/))
- Enabled Steam Patch for any hardware other than Steam Deck
    - Users no longer have to select "Native" in a game properties in Game Mode.
- Added nautilus integration for GSConnect. (KDE Connect for GNOME)
    - Default on Steam Deck, HTPC, and Handheld PC images.
    - Edit `/etc/default/cec-control` to change behavior.
- Added Winesync/Fastsync/NTSync support.
- Disabled split lock mitigation for increased gaming performance. (Thanks [Saber J2X!](https://github.com/SaberJ2X))
- Added message to plymouth during long `bazzite-hardware-setup` steps.
- RazorGenie is now added to OpenRazor installation in the Bazzite Portal.
- Added icons for Windows applications (`.exe`, `.msi`, etc.) in the file manager.
- Enable automounting of hugepages with 1GB pagesize if specific kernel arguments are present.
- Include `vulkan-tools` and `clinfo` in all images.
- Added virtual audio channels for special usecases.
- Added Virtual Surround 7.1 setup to `just`.
    - Added a basic virtual surround 7.1 config using ASH Control Room 1.
- Added support for [Looking Glass](https://github.com/gnif/LookingGlass).
- Added [Resources](https://github.com/nokyan/resources), [AppImage Pool](https://github.com/prateekmedia/appimagepool) and [Pika Backup](https://gitlab.gnome.org/World/pika-backup) to Bazzite Portal.
- Added [Warehouse](https://github.com/flattool/warehouse) as a preinstalled application to manage Flatpaks.
- Both KDE and GNOME can now screen share properly under Wayland.
- GNOME images now switch to new Logo Menu fork by Bazzite.
- GNOME images now have a "Add to Steam" option to right click menu.
- New Tailscale [extension](https://github.com/maxgallup/tailscale-status) for GNOME images.
- Added default dash application assignments for GNOME images.
- Use new privileged user setup script for certain tasks.
- Increased priority of sysctl changes.
- Added CharmVHS & CharmGUM for future use in `just` commands. 
- Doubled zram size on 32GB of RAM hardware modded Steam Decks.
- Deck images have Steam shortcuts for Waydroid including icons and input settings.
- Deck images have a new SteamOS Nested Desktop feature.
    - GNOME images cannot launch any application in these nested desktop sessions currrently due to upstream issues. 
- Deck images now have increased ZRAM size to 4GB by defaul & performance improvements. (Thanks [Saber J2X](https://github.com/SaberJ2X)!) 
- Deck images now block additional AMD watchdog kernel modules to improve performance.
    - We also added the option to enable these watchdog kernel modules back
        - `just enable-watchdog` to enable and `just disable-watchdog` to disable.
- Deck images switched to stable Decky Loader releases.


### Bug Fixes
- Fixed boot issues.
- Tons of `steam-patch` fixes.
    - HandyGCCS is now added back too.
- Corrected hostname check. (Thanks [szescxz](https://github.com/szescxz)!) 
- Moved obs-vkcapture to Nvidia & Deck images only.
- Added some safety checks to ensure flathub is enabled 
- Start Solaar minimized by default on login.
- Tidy up Nix installation.
- Moved fstab changes to prevent any issues on a rebase.
- Enabled initramfs generation for LUKS. 
- Remove non-working gsetting call.
- Minor cleanup to `just`.
- Fixed EmuDeck not working on Steam Deck imgaes.
- Increased default battery limit on Steam Deck images.
- Fixed a lot of issues with Nvidia images.
- Fixed bluetooth controllers disconnecting.
- Fixed Bazzite Portal issues.
- Fixed `just reset-waydroid` command not working. 
- Fixed OpenTabletDriver not installing in Bazzite Portal.
- Fixed Krita installing Ardour in the Bazzite Portal.
- Fixed missing first-launch call in Waydroid.
- Fixed zram-resize.
- Display an error if a Flatpak fails to install in the Bazzite Portal.
- Corrected issue with screen rotation on non-deck hardware using the Steam Deck images.
- Corrected mismatched curl version in install.
- Dropped DNS over TLS and SNTP due to reported issues/edge cases.
    - Will re-introduce as an option in Bazzite Portal at a later time.
- Removed `rd.luks.options=discard` & use `--append-if-missing` for kernel arguments.
- GNOME images have restored [appindicator extension](https://github.com/ubuntu/gnome-shell-extension-appindicator).

[Full changelog](https://github.com/ublue-os/bazzite/commits/main)

<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) 
