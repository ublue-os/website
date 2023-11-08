---
date: 2023-11-08
comments: true
authors: 
  - KyleGospo
  - EyeCantCU
categories:
  - bazzite
links: 
  - Bazzite: https://www.bazzite.gg
---

# Bazzite 2.0

![Tagline](https://github.com/ublue-os/website/assets/121328689/35466b14-9c11-4e04-8584-ce4cc3d7d93d)

![20](https://github.com/ublue-os/website/assets/121328689/8a706c0d-802d-4a39-bed8-74ac2a52f4bf)

## Welcome to "Phase II" of Bazzite

<hr>

<p style="text-align: center; font-weight: 600; color: red">ATTENTION:</p>

If you installed Bazzite previously with the older ISOs then **YOU MAY BE STUCK ON FEDORA 38 BUILDS IF THE INSTALLER INSTALLED A `:38` IMAGE AND NOT A `:latest` IMAGE!**  If you are unsure and feel like you are not up to date, open a host terminal and enter `rpm-ostree status`.  If it says that your deployment is on `:38` then you need to follow these instructions!

Open a host terminal and enter the command below for the image you're using.

- Bazzite AMD/Intel Desktop: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite:latest`  
- Bazzite Nvidia Desktop: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-nvidia:latest`  
- Bazzite AMD/Intel Desktop GNOME: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-gnome:latest`
- Bazzite Nvidia Desktop GNOME: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-gnome-nvidia:latest`
- Bazzite Steam Deck/HTPC/Handheld PC: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck:latest`
- Bazzite Steam Deck/HTPC/Handheld PC GNOME: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck-gnome:latest`

For specific images that relate to hardware (Framework, Microsoft Surface, ASUS, etc.) see the [full image list](https://universal-blue.org/images/#latest) and make sure "latest" is selected.

After you enter the command, wait for it to finish (this will take a while), and reboot.  You should now get the latest updates for Bazzite.  

We apologize for the inconvenience if you had to rebase, but you will NOT lose userdata rebasing to the `:latest` branch of the current image that you are on.

If you tested the Fedora 39 builds of Bazzite early, then you need to rebase back to `:latest` to be updated to future Bazzite versions as well.

Also desktop portal issues are happening currently: `systemctl restart --user xdg-desktop-portal` if you experience issues with the file picker.

<hr>

It has been nearly 3 months later since releasing Bazzite to the public, and since then the team and the community has added tons of new features, enhancements, and bug fixes to the images. 

The functionality is already there for Bazzite and utilizing [new desktop model](https://www.youtube.com/watch?v=vZ1LRe_foJY) can be successful, and now the focus is on having a better user experience.

The new Bazzite builds have now upgraded to Fedora Linux 39.  The project is now at a point where it is completely functional as is on standard hardware (and the Steam Deck.)

Bazzite's original purpose was to be a version of SteamOS that allowed for flexible functionality for users who found SteamOS to be too limiting, or felt SteamOS couldn't be a proper desktop Linux operating system.  The project has now expanded has now grown and expanded drastically to work on multiple hardware configurations outside of the Steam Deck, and being a desktop SteamOS clone.  

We would like to thank our growing community for supporting and sending feedback which helps us improve the project.

# What is Bazzite?

Bazzite is an OCI image that serves as an alternative operating system for the [Steam Deck](https://www.steamdeck.com/), and a ready-to-game SteamOS-like for desktop computers and living room home theater PCs.

Bazzite is built from [ublue-os/main](https://github.com/ublue-os/main) and [ublue-os/nvidia](https://github.com/ublue-os/nvidia) using [Fedora](https://fedoraproject.org/) technology, which means expanded hardware support, built in drivers, mutli-media codecs are included.  For more information on what makes Bazzite unique, check out the [documentation](/images/bazzite/FAQ/#how-does-bazzite-differ-from-other-linux-distributions).


![KDE Vapor Theme](https://github.com/ublue-os/website/assets/121328689/24d8f60d-7610-4f00-a7cc-1d6868f0902c)
<p style="text-align: center;font-weight: bold;font-size: 16px">Bazzite running KDE Plasma</p>

## Bazzite Features

### Features for All of the Bazzite Images

- Proprietary Nvidia drivers pre-installed.
- Full hardware accelerated codec support for H264 decoding.
- Full support for AMD's ROCM OpenCL/HIP run-times.
- [xone](https://github.com/medusalix/xone), [xpadneo](https://github.com/atar-axis/xpadneo), and [xpad-noone](https://github.com/ublue-os/xpad-noone) drivers for Xbox controllers.
- Full support for [DisplayLink](https://www.synaptics.com/products/displaylink-graphics).
- Includes Valve's KDE themes from SteamOS.
- [LatencyFleX](https://github.com/ishitatsuyuki/LatencyFleX), [vkBasalt](https://github.com/DadSchoorse/vkBasalt), [MangoHud](https://github.com/flightlessmango/Mangohud), and [OBS VkCapture](https://github.com/nowrep/obs-vkcapture) installed and available by default
- Support for [Wallpaper Engine](https://www.wallpaperengine.io/en). <sub><sup>(Only on KDE)</sup></sub>
- [ROM Properties Page shell extension](https://github.com/GerbilSoft/rom-properties) included.
- Full support for [Winesync/Fastsync/NTsync](https://github.com/Frogging-Family/wine-tkg-git/issues/936).
- [Distrobox](https://github.com/89luca89/distrobox) preinstalled with automatic updates for created containers.
- Automated `duperemove` and `rmlint` services for reducing the disk space used by wine prefix contents.
- Support for HDMI CEC via [libCEC](https://libcec.pulse-eight.com/).
- [System76-Scheduler](https://github.com/pop-os/system76-scheduler) preinstalled, providing automatic process priority tweaks to your focused application and keeping CPU time for background processes to a minimum.
- Customized System76-Scheduler config with additional rules.
- Uses [Google's BBR TCP congestion control](https://github.com/google/bbr) by default.
- [Input Remapper](https://github.com/sezanzeb/input-remapper) preinstalled and enabled. <sub><sup>(Available but default-disabled on the Deck variant)</sup></sub>
- Bazzite Portal provides an easy way to install numerous applications and tweaks, including installing [CoreCtrl](https://gitlab.com/corectrl/corectrl) and [GreenWithEnvy](https://gitlab.com/leinardi/gwe).
- [Nix](https://nixos.org/) package manager with [Fleek](https://getfleek.dev/) optionally available for install via Bazzite Portal.
- [Brew](https://brew.sh/) package manager optionally available for install via Bazzite Portal.
- [Waydroid](https://waydro.id/) preinstalled for running Android apps. Future releases will offer to set this up for you through Bazzite Portal. <sub><sup>(Not available on Nvidia builds)</sup></sub>
- Manage applications using [Flatseal](https://github.com/tchx84/Flatseal), [Warehouse](https://github.com/flattool/warehouse), and [Gear Lever](https://github.com/mijorus/gearlever).
- [OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB) i2c-piix4 and i2c-nct6775 drivers for controlling RGB on certain motherboards.
- [OpenRazer](https://openrazer.github.io) drivers built in, Select OpenRazer in Bazzite Portal or run `just install-openrazer` in a terminal to begin using it.
- [OpenTabletDriver](https://opentabletdriver.net/) udev rules built in, with the full software suite installable via Bazzite Portal or by running `just install-opentabletdriver` in a terminal.
- [GCAdapter_OC](https://github.com/hannesmann/gcadapter-oc-kmod) driver for overclocking Nintendo's Gamecube Controller Adapter to 1000hz polling.
- Out of the box support for [Wooting](https://wooting.io/) keyboards.
- Built in support for Southern Islands <sub><sup>(HD 7000)</sup></sub> and Sea Islands <sub><sup>(HD 8000)</sup></sub> AMD GPUs under the `amdgpu` driver.
- A fix is available for [a TF2 bug](https://github.com/ValveSoftware/Source-1-Games/issues/5043) that makes the game crash on launch - `just patch-tf2-tcmalloc`
- [XwaylandVideoBridge](https://invent.kde.org/system/xwaylandvideobridge) is available for Discord screensharing on Wayland. <sub><sup>(Only on KDE)</sup></sub>

![Waydroid](https://github.com/ublue-os/website/assets/121328689/11f29b2f-af00-420e-9cf0-1ff16be2f275)
<p style="text-align: center;font-weight: bold;font-size: 16px">Bazzite can run Android inside of a container.</p>

### Features for Desktop Images

Common variant available as `bazzite`, suitable for desktop computers.

- Runs Steam and Lutris in a [custom Arch Linux OCI](https://github.com/ublue-os/bazzite-arch/) via Distrobox. <sub><sup>(Except on Nvidia)</sup></sub>
- Automatic updates for the OS, Flatpaks, Nix packages <sup><sub>(Via Fleek)</sub></sup>, and all Distrobox containers.


### Features for Steam Deck, Home Theater PCs, & Handheld PC Images

![Steam Game Mode](https://github.com/ublue-os/website/assets/121328689/4084a52a-b7c9-4ec7-a27f-87a6104b4dea)
<p style="text-align: center;font-weight: bold;font-size: 16px">Game Mode functions as expected.</p>

> [!IMPORTANT]  
Devices that are NOT the Steam Deck can still use the bazzite-deck images, but must use an AMD/Intel GPU.

Variant designed for usage as an alternative to SteamOS on the Steam Deck, and for a console-like experience on HTPCs, available as `bazzite-deck`:

- Directly boots to Gamemode matching SteamOS's behavior.
- **Automatic `duperemove` greatly trims the size of compatdata.**
- **Latest version of Mesa creates smaller shader caches and does not require them to prevent stutter.**
- **Able to be booted even if the drive is full.**
- **Support for every language supported by upstream Fedora.**
- Optionally use Wayland on the desktop with [support for Steam input](https://github.com/Supreeeme/extest).
- Features ported versions of most SteamOS packages, including drivers, firmware updaters, and fan controllers [from the evlaV repository](https://gitlab.com/evlaV).
- Patched Mesa for proper framerate control from Gamescope.
- Comes with patches from [SteamOS BTRFS](https://gitlab.com/popsulfr/steamos-btrfs) for full BTRFS support for the SD card by default.
- Ships with a ported copy of [SDGyroDSU](https://github.com/kmicki/SteamDeckGyroDSU), enabled by default.
- Option to install [Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader), [EmuDeck](https://www.emudeck.com/), [RetroDECK](https://retrodeck.net/), and [ProtonUp-Qt](https://davidotek.github.io/protonup-qt/), among numerous other useful packages on installation.
- Custom update system allows for the OS, Flatpaks, Nix packages <sup><sub>(Via Fleek)</sub></sup>, and Distrobox images to be updated directly from the Gamemode UI.
- Built in support for Windows dual-boot thanks to Fedora's installation of GRUB being left intact.
- Update break something? Easily roll back to the previous version of Bazzite thanks to `rpm-ostree`'s rollback functionality. You can even select previous images at boot.
- Steam and Lutris preinstalled on the image as layered packages.
- [Discover Overlay](https://github.com/trigg/Discover) for Discord pre-installed and automatically launches in both Gamemode and on the Desktop if Discord is installed. [View the official documentation here](https://trigg.github.io/Discover/bazzite).
- Uses ZRAM<sub><sup>(4GB)</sup></sub> with the ZSTD compression algorithm by default with the option to switch back to a 1GB swap file and set a custom size for it if desired.
- Kyber I/O scheduler to prevent I/O starvation when installing games or during background `duperemove` and `rmlint` processes.
- Applies SteamOS's kernel parameters.
- Color calibrated display profiles for matte and reflective Steam Deck screens included.
- Default-disabled power-user features, including:
    - Service for low-risk undervolting of the Steam Deck via [RyzenAdj](https://github.com/FlyGoat/RyzenAdj) and [Ryzen SMU](https://gitlab.com/leogx9r/ryzen_smu), see `ryzenadj.service` and `/etc/default/ryzenadj`.
    - Service for limiting the max charge level of the battery, see `batterylimit.service` and `/etc/default/batterylimit`. <sup><sub>(Works even when the device is off)</sub></sup>
    - Built in support for display overclocking. For example, add `GAMESCOPE_OVERRIDE_REFRESH_RATE=40,70` to `/etc/environment`.
    - Ability to enable Wayland on the desktop if desired by editing `/etc/default/desktop-wayland`.
    - 32GB RAM mod your Steam Deck? Enjoy double the maximum VRAM amount, automatically applied. <sup><sub>(Can you share your soldering skills?)</sub></sup>
- Steam Deck hardware-specific services can be disabled by running `just disable-deck-services` in the terminal, useful for trying this image on other handhelds or for use on HTPCs.


### Features for GNOME Images (Alternative Desktop Environment)

![GNOME Vapor Theme](https://github.com/ublue-os/website/assets/121328689/985c1707-8e37-4e54-ae02-2258ef536ebc)
<p style="text-align: center;font-weight: bold;font-size: 16px">Bazzite running GNOME.</p>

Builds with the GNOME desktop environment are available in both desktop and deck flavors. These builds come with the following additional features:

- [Variable refresh rate support and fractional scaling enabled under Wayland](https://gitlab.gnome.org/GNOME/mutter/-/merge_requests/1154).
- Custom menu in the top bar for returning to game mode, launching Steam, and opening a number of useful utilities. <sub><sup>(Only on Steam Deck builds)</sup></sub>
- [GSConnect](https://extensions.gnome.org/extension/1319/gsconnect/) preinstalled and ready to use.
- Features optional Valve-inspired themes matching Vapor and VGUI2 from SteamOS.
- [Hanabi extension](https://github.com/jeffshee/gnome-ext-hanabi) included to offer similar features to Wallpaper Engine in KDE.
- Numerous optional extensions pre-installed, including [important user experience fixes](https://www.youtube.com/watch?v=nbCg9_YgKgM).
- Automatic updates for the [Firefox GNOME theme](https://github.com/rafaelmardojai/firefox-gnome-theme) and [Thunderbird GNOME theme](https://github.com/rafaelmardojai/thunderbird-gnome-theme). <sup><sub>(If installed)</sub></sup>

### Features from Upstream

#### Universal Blue

- Flathub is enabled by default.
- [`just`](https://github.com/casey/just) commands for convenience.
- Multi-media codecs out of the box.
- Rollback Bazzite from any build within the last 90 days.

#### Features from Fedora Linux (Kinoite & Silverblue)

- A rock solid and stable base.
- System packages stay relatively up to date.
- Can layer Fedora packages to the image without losing them between updates.
- Security focused with [SELinux](https://github.com/SELinuxProject/selinux) preinstalled and configured.
- The ability to rebase to different Fedora libostree images, if desired, without losing user data.
- Printing support thanks to [CUPS](https://www.cups.org/) being preinstalled.

## Current Status

Bazzite is in a much better state than it was at the 1.0 release.  The first couple of months have been working towards having a stable experience and adding new features that sets this image apart from other desktop Linux distributions.

[Installer issues](https://universal-blue.org/images/bazzite/FAQ/#i-am-having-issues-installing-bazzite-on-my-hardware-whats-going-on) from upstream still plague the user experience unfortunately.  However, [things are looking up](https://github.com/osbuild/osbuild/pull/1418), so perhaps in the near future this will not be an issue anymore.  Post-installation, you should be able to use Bazzite on your device smoothly, but please let us know if you experience any issues.

## Install Bazzite Today!

Start with the documentation and make sure you follow the [installation instructions](https://universal-blue.org/images/bazzite/installation/) carefully. The installation process is still considered incomplete, but hopefully these issues are solved soon.

Read Bazzite's [FAQ](https://universal-blue.org/images/bazzite/FAQ/) to if you have questions on the project.  

Check out our [newsletters](https://universal-blue.org/blog/category/bazzite/) that get published on a regular basis for updates on the project.

Install Bazzite today from the latest ISO on the [releases page](https://github.com/ublue-os/bazzite/releases).


## Special Thanks

Bazzite is a community effort and wouldn't exist without everyone's support. Below are some of the people who've helped us along the way:

- [rei0260](https://discord.com/users/rei0260) - For creating our logo and overall branding.
- [evlaV](https://gitlab.com/evlaV) - For making Valve's code available and for being [this person](https://xkcd.com/2347/).
- [ChimeraOS](https://chimeraos.org/) - For gamescope-session and for valuable support along the way.
- [Jovian-NixOS](https://github.com/Jovian-Experiments) - For supporting us with technical issues and for creating a similar project. Seriously, go check it out. It's our Nix-based cousin.
- [Steam Deck Homebrew](https://deckbrew.xyz) - For choosing to support distributions other than SteamOS despite the extra work, and a special thanks to [PartyWumpus](https://github.com/PartyWumpus) for getting Decky Loader working with SELinux for us.
- [cyrv6737](https://github.com/cyrv6737) - For the initial inspiration and the base that became bazzite-arch.

## Join The Community!


Bazzite is an open source project, contributions and feedback accepted! Check out the [Contributor's Guide](https://universal-blue.org/images/bazzite/CONTRIBUTING/) to get started.

You can find us on the [Universal Blue Discord](https://discord.gg/f8MUghG5PB).

You can also discuss on our [Github Discussions](https://github.com/orgs/ublue-os/discussions/categories/bazzite) for any new features or issues you're experiencing with Bazzite.

<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM169.8 165.3c7.9-22.3 29.1-37.3 52.8-37.3h58.3c34.9 0 63.1 28.3 63.1 63.1c0 22.6-12.1 43.5-31.7 54.8L280 264.4c-.2 13-10.9 23.6-24 23.6c-13.3 0-24-10.7-24-24V250.5c0-8.6 4.6-16.5 12.1-20.8l44.3-25.4c4.7-2.7 7.6-7.7 7.6-13.1c0-8.4-6.8-15.1-15.1-15.1H222.6c-3.4 0-6.4 2.1-7.5 5.3l-.4 1.2c-4.4 12.5-18.2 19-30.6 14.6s-19-18.2-14.6-30.6l.4-1.2zM224 352a32 32 0 1 1 64 0 32 32 0 1 1 -64 0z"/></svg>](https://universal-blue.org/images/bazzite/FAQ/)
