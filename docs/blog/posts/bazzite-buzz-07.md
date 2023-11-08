---
date: 2023-11-08
comments: true
authors: 
  - nicknamenamenick
categories:
  - bazzite
links:
  - Bazzite Commits: https://github.com/ublue-os/bazzite/commits/main
  - Bazzite 2.0: https://universal-blue.org/blog/2023/11/08/bazzite-20/
---

# Bazzite Buzz #7: Fedora 39 Builds Out Now

![bg](https://github.com/ublue-os/website/assets/121328689/830c2afb-1796-43ef-a093-90449503f81c)

<hr>

<p style="text-align: center; font-weight: 600; color: red">ATTENTION:</p>

YOU MAY BE STUCK ON FEDORA 38 BUILDS IF THE INSTALLER INSTALLED A `:38` IMAGE AND NOT A `:latest` IMAGE!  Open a host terminal and enter the command below for the image you're using.

- Bazzite AMD/Intel Desktop: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite:latest`  
- Bazzite Nvidia Desktop: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-nvidia:latest`  
- Bazzite AMD/Intel Desktop GNOME: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-gnome:latest`
- Bazzite Nvidia Desktop GNOME: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-gnome-nvidia:latest`
- Bazzite Steam Deck/HTPC/Handheld PC: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck:latest`
- Bazzite Steam Deck/HTPC/Handheld PC GNOME: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck-gnome:latest`

For specific images that relate to hardware (Framework, Microsoft Surface, ASUS, etc.) see the [full image list](https://universal-blue.org/images/#latest) and make sure to select "latest" is selected.

After you enter the command, wait for it to finish (this will take a while), and reboot.  You should now get the latest updates for Bazzite.  

We apologize for the inconvenience if you had to rebase, but you will NOT lose userdata rebasing to the `:latest` branch of the current image that you are on.

If you tested the Fedora 39 builds of Bazzite early, then you need to rebase back to `:latest` to be updated to future Bazzite versions as well.
<hr>

![20](https://github.com/ublue-os/website/assets/121328689/d279494f-86c2-479e-a2b9-efd69f0783e6)

### Welcome to Bazzite 2.0 (New ISOs out now!)

Bazzite is a custom image of [**Fedora Linux 39**](https://www.fedoraproject.org/) utilizing Universal Blue's custom image framework designed to bring users the best in Linux gaming for their PCs, including the Steam Deck and other handheld PCs. Bazzite's newsletters highlight all of the work we have been doing to bring gamers the best features ready to go for their PCs, home theater setups, and handheld gaming devices.

If you are new to the project then here's how this technology works:  Bazzite and other [Universal Blue](https://universal-blue.org/) images follow the [continuous delivery](https://continuousdelivery.com/) methodology of development which means we're constantly adding new features and squashing bugs to the image through updates. These updates also include anything directly from upstream (Fedora and Universal Blue) and upgrades from the [packages](https://github.com/ublue-os/bazzite#custom-packages) we include.

Today's newsletter focuses primarily on the state of Bazzite today and some new features to the project, including the migration from Fedora 38 to Fedora 39 in our builds.  As always, we have the changelog for all of the new features and bug fixes at the end of the newsletter.


## Bazzite on Fedora 39

![GNOME45](https://github.com/ublue-os/website/assets/121328689/95a6a8bf-0199-412a-abc5-ae456c2cf67f)
<p style="text-align: left;font-weight: bold;font-size: 14px">GNOME 45 running on Bazzite, which is now using Fedora 39 as a base.</p>

Bazzite has upgraded from Fedora 38 to Fedora 39 recently.  This means all of the changes from Fedora Linux 39 will already be in Bazzite once you update to the latest build.  

The highlights of this release are mostly tied to performance, package upgrades, and for those using GNOME images, it is now upgraded to version 45.  

The upgrade is automatically done through an update on desktop images and will be there when you reboot.  The Steam Deck centric images, the images with Game Mode, will require you to update in Game Mode.  Of course, you can open the terminal and enter `ublue-update` and `rpm-ostree update` to update through the terminal if you prefer to upgrade immediately.  Although there has been inconsistent reports of users stuck on Fedora 38 builds.  Please refer to the top of the newsletter to fix that.


## Lenovo Legion Go Support

![neofetch](https://github.com/ublue-os/website/assets/121328689/d9fe6443-d941-4c1b-bf81-b0ce805a244b)
<p style="text-align: left;font-weight: bold;font-size: 14px">Bazzite on the Lenovo Legion handheld PC.  Photo taken by Oteresk.</p>

That's right!  The Lenovo Legion Go can run Bazzite using the Steam Deck / HTPC images.  Install the `bazzite-deck` or `bazzite-deck-gnome` image on it to see it in action for yourself. 

Lenovo has a consistent track record with hardware with fantastic Linux support.  Eventually there might be a dedicated Legion Go image depnding on the circumstances.  When this is released, you can rebase to the Legion Go image without having to reinstall.  We will keep the community up to date if this happens, but for now you can use it with the generic Steam Deck images with some caveats, but surely as time goes it will improve.

![gamemode](https://github.com/ublue-os/website/assets/121328689/c7aceab9-c980-4301-b341-519476e8d48b)
![ingame](https://github.com/ublue-os/website/assets/121328689/26c108fb-76d2-434b-991a-c345264d9f0f)
<p style="text-align: left;font-weight: bold;font-size: 14px">Lenovo Legion Go running Game Mode and in-game! Photos taken by Oteresk.</p>

Now, for some bad news.  Asus ROG Ally support progress has been halted due to a required kernel module that is not cooperating with the Ally image.  We recommend at this time to use [ChimeraOS](https://chimeraos.org/) and [Nobara](https://nobaraproject.org/) if you want a SteamOS-like experience on the Ally.  This might be resolved in the future, but this is the hard truth presently that the project is facing with this handheld.  It may be revisited at a later time, and anyone who owns this handheld can attempt to figure out the issues if they feel up for the challenge.

## Switching Update Branches & Bug Fixes

Users can now switch to different update branches of Bazzite. 
- Latest (**default**, **stable**)  
- Testing
- Unstable (**not recommended**)

Latest is the default branch and what we generally recommend for most users to stay on.  Testing is a preview of what's to come, and unstable is only recommended for advanced users and is exactly how it sounds.

[Waydroid](https://waydro.id/) has improved since it was first packaged in Bazzite.  Check out the [updated guide](https://universal-blue.org/images/bazzite/waydroid/) for setting it up if you want to run Android applications.

Lots of bug also have been squashed the last couple of weeks.  OpenRazor should function properly now once installed through the Bazzite Portal.  Lutris should no longer complain about missing Wine dependencies, and Nix applications should have icons.

## DaVinci Resolve Container & Bluefin Beta

Slightly off-topic from Bazzite, but some related news that applies to the Universal Blue project as a whole.

For the video editing enthusiasts out there, if you use DaVinci Resolve and want to get it working well on Bazzite or any Universal Blue image, check out this [article](https://zelikos.dev/blog/posts/2023-09-07-davincibox) that goes over in detail how to get DaVinci Resolve working inside of its own container.

![Bluefin](https://github.com/ublue-os/website/assets/121328689/3bf84bd7-5681-459f-930f-dee4b9f3470b)
<p style="text-align: left;font-weight: bold;font-size: 14px">Bluefin showcase by Justin Garrison.</p>

While we're on the topic of Universal Blue, [Bluefin](https://projectbluefin.io/) is another Universal Blue image centered around an Ubuntu-like experience, but using the Fedora Linux technology that Bazzite users are already familiar with.  A great image to install on a laptop or workstation.  If you want a developer-focused OS in the same nature as Bazzite, then give it a shot even if it's in a virtual machine for testing purposes!  You can even [make your own image too](https://universal-blue.org/guide/fork-your-own/)!

## Closing Thoughts

Bazzite and its community has grown extraordinarily since we first started.  The project is now established and can move forward focusing on stability and hardware support.  The future of Bazzite will be focused on keeping up with feature parity of SteamOS, getting other hardware to work on it, and taking cues from the feedback we have received to make a better image for everyone.

There has also been users in our community who would prefer not to use Discord as a communication method for support or discussion.  We do have a [Github Discussions](https://github.com/orgs/ublue-os/discussions/categories/bazzite) forum, but that's not an alternative to an instant messaging platform like Discord.  A user has [suggested](https://github.com/ublue-os/main/issues/388) to have an unofficial [Matrix](https://matrix.to/#/#universal-blue:matrix.org) room.  However, the maintainers of the images may not be as present, if at all, for any alternative means of communication outside of Discord and the Github discussions.  This is detrimental for support, but we are not against a community forming outside of the official communication channels discussing and helping each other surrounding the Universal Blue projects including Bazzite

Currently, one of the major growing pains is the installation process.  If you do run into installation issues, then please check out the workarounds listed [here](https://universal-blue.org/images/bazzite/FAQ/#i-am-having-issues-installing-bazzite-on-my-hardware-whats-going-on).  Bazzite still has the feeback [**survey**](https://opnform.com/forms/your-bazzite-experience-sohzei) open if anyone who hasn't taken it yet is still interested. There is also a [Github discussion](https://github.com/orgs/ublue-os/discussions/246) open for feedback on the project too.


We would like to thank our community for helping the project grow into what it is today.  New users who want to give Bazzite a try, here is the the [**latest releases**](https://github.com/ublue-os/bazzite/releases). Check out the [installation guide](https://universal-blue.org/images/bazzite/installation/) and [FAQ](https://universal-blue.org/images/bazzite/FAQ/), and if you experience any issues, then please refer to our [issue tracker](https://github.com/ublue-os/bazzite/issues).  Also, discuss any feature requests or questions you have about Bazzite [here](https://github.com/orgs/ublue-os/discussions/categories/bazzite).


## Changelog

### New Features
- Bazzite has now upgraded from Fedora 38 to Fedora 39, here are the major changes:
    - GNOME is now on version 45
        - Check out all the major changes [here](https://release.gnome.org/45/).
    - Newer base packages.
    - Performance improvements.
    - Colored Bash prompt.
    - [Full changelog for Fedora 39](https://www.fedoraproject.org/wiki/Releases/39/ChangeSet)
- Newly updated [ISOs](https://github.com/ublue-os/bazzite/releases) for Fedora 39.
- Lenovo Legion GO support.
    - Hardware control. 
    - Controller support.
    - Orientation fixes.
- Support for switching update branches.
    - Latest (Default), Testing, and Unstable (Not recommended).
- Waydroid support has improved.
    -  Hybrid graphic support out of the box.
    -  Wayland launcher will now automatically initialize.
    -  Set density and Gralloc before launch.
- Added [Gamescope-Session-Plus](https://github.com/ChimeraOS/gamescope-session).
- Added [gperftools](https://github.com/gperftools/gperftools) for older Source engine titles.
- Added [kdeplasma-addons](https://github.com/ublue-os/bazzite/commit/69c78de60eeb0a6e6ed83079f29cd497a10d8506) for KDE images.
- Added [steam-proton-mf-wmv utility](https://github.com/scaronni/steam-proton-mf-wmv/).
- Added [LatencyFleX-Installer](https://github.com/Shringe/LatencyFleX-Installer/).
- Added [QTVirtualKeyboard](https://github.com/qt/qtvirtualkeyboard) for SDDM for Steam Deck / HTPC images.
- Added [vk_hdr_layer ](https://github.com/Drakulix/VK_hdr_layer) for experimental HDR support.
- Added support for using `ryzenadj` for other hardware from [corando98's steam-patch fork](https://github.com/corando98/steam-patch).


### Bug Fixes
- Fixed a mistaken dependency issue in Lutris.
- Fixed OpenRazer not installing in the Bazzite Portal.
- Dropped VHS, keep gum.
- Replaced TF2 fix with `LD_PRELOAD` method.
- Fixed nested GNOME sessions for most applications (besides Flatpak Firefox).
- Fixed icons not appearing for Nix applications.
- Switched to layered OpenRazor due to issues with Distrobox containerization.
- Fixed several ASUS build issues.
- Added Minimum-free ZRAM configuration.
- Massively improved steamos-priv-write.
- Bazzite Portal now displays Bazzite's page on Universal Blue's website when you click on "Website".
- Improve BIOS update disabling feature for Steam Deck images.
- Restored Simple Direct Rendering Manager for Steam Deck images.

<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM169.8 165.3c7.9-22.3 29.1-37.3 52.8-37.3h58.3c34.9 0 63.1 28.3 63.1 63.1c0 22.6-12.1 43.5-31.7 54.8L280 264.4c-.2 13-10.9 23.6-24 23.6c-13.3 0-24-10.7-24-24V250.5c0-8.6 4.6-16.5 12.1-20.8l44.3-25.4c4.7-2.7 7.6-7.7 7.6-13.1c0-8.4-6.8-15.1-15.1-15.1H222.6c-3.4 0-6.4 2.1-7.5 5.3l-.4 1.2c-4.4 12.5-18.2 19-30.6 14.6s-19-18.2-14.6-30.6l.4-1.2zM224 352a32 32 0 1 1 64 0 32 32 0 1 1 -64 0z"/></svg>](https://universal-blue.org/images/bazzite/FAQ/)
