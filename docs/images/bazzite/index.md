# Bazzite

<p align="center">
  <img src="https://github.com/ublue-os/bazzite/blob/main/repo_content/Bazzite_Tagline.svg?raw=true"/>
</p>

[![build-bazzite](https://github.com/ublue-os/bazzite/actions/workflows/build.yml/badge.svg)](https://github.com/ublue-os/bazzite/actions/workflows/build.yml)

## About & Features

Bazzite is an OCI image that serves as an alternative operating system for the [Steam Deck](https://www.steamdeck.com/), and a ready-to-game SteamOS-like for desktop computers and living room home theater PCs.

Bazzite is built from [ublue-os/main](https://github.com/ublue-os/main) and [ublue-os/nvidia](https://github.com/ublue-os/nvidia) using [Fedora](https://fedoraproject.org/) technology, which means expanded hardware support and built in drivers are included. Additionally, Bazzite adds the following features:

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
- [OpenRazer](https://openrazer.github.io) drivers built in, Select OpenRazer in Bazzite Portal or run `ujust install-openrazer` in a terminal to begin using it.
- [OpenTabletDriver](https://opentabletdriver.net/) udev rules built in, with the full software suite installable via Bazzite Portal or by running `ujust install-opentabletdriver` in a terminal.
- [GCAdapter_OC](https://github.com/hannesmann/gcadapter-oc-kmod) driver for overclocking Nintendo's Gamecube Controller Adapter to 1000hz polling.
- Out of the box support for [Wooting](https://wooting.io/) keyboards.
- Built in support for Southern Islands <sub><sup>(HD 7000)</sup></sub> and Sea Islands <sub><sup>(HD 8000)</sup></sub> AMD GPUs under the `amdgpu` driver.
- A fix is available for [a 32-bit Source 1 engine game bug <sub><sup>(IE: TF2)</sup></sub>](https://github.com/ValveSoftware/Source-1-Games/issues/5043) that makes the game crash on launch - `ujust patch-source1-tcmalloc`
- [XwaylandVideoBridge](https://invent.kde.org/system/xwaylandvideobridge) is available for Discord screensharing on Wayland.

### Desktop

Common variant available as `bazzite`, suitable for desktop computers.

- Automatic updates for the OS, Flatpaks, Nix packages <sup><sub>(Via Fleek)</sub></sup>, and all Distrobox containers.

> [!IMPORTANT]  
> **ISOs can be downloaded from our releases page [here](https://github.com/ublue-os/bazzite/releases), and a helpful install guide can be found [here](https://universal-blue.org/images/bazzite/installation/).**

If you're on an existing Universal Blue image follow [these instructions](https://universal-blue.org/images/#image-list). To rebase an existing upstream Fedora Silverblue/Kinoite ostree system to this image:

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite:latest
```

or for devices with Nvidia GPUs:

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite-nvidia:latest
```

**For users with Secure Boot enabled:** Run `ujust enroll-secure-boot-key` and enter the password `ublue-os` if prompted to enroll the required key.

### Steam Deck/Home Theater PCs (HTPCs)
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
- Steam Deck hardware-specific services can be disabled by running `ujust disable-deck-services` in the terminal, useful for trying this image on other handhelds or for use on HTPCs.

> [!WARNING]  
> **Due to an upstream bug, Bazzite cannot be used on Steam Decks with 64GB eMMC storage at this time. Upgrading the storage resolves the issue.**

> [!IMPORTANT]  
> **ISOs can be downloaded from our releases page [here](https://github.com/ublue-os/bazzite/releases), and a helpful install guide can be found [here](https://universal-blue.org/images/bazzite/installation/).**

If you're on an existing Universal Blue image follow [these instructions](https://universal-blue.org/images/#image-list). To rebase an existing upstream Fedora Silverblue/Kinoite ostree system to this image: 

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite-deck:latest
```

### GNOME

Builds with the GNOME desktop environment are available in both desktop and deck flavors. These builds come with the following additional features:

- [Variable refresh rate support and fractional scaling enabled under Wayland](https://gitlab.gnome.org/GNOME/mutter/-/merge_requests/1154).
- Custom menu in the top bar for returning to game mode, launching Steam, and opening a number of useful utilities. <sub><sup>(Only on Steam Deck builds)</sup></sub>
- [GSConnect](https://extensions.gnome.org/extension/1319/gsconnect/) preinstalled and ready to use.
- Features optional Valve-inspired themes matching Vapor and VGUI2 from SteamOS.
- [Hanabi extension](https://github.com/jeffshee/gnome-ext-hanabi) included to offer similar features to Wallpaper Engine in KDE.
- Numerous optional extensions pre-installed, including [important user experience fixes](https://www.youtube.com/watch?v=nbCg9_YgKgM).
- Automatic updates for the [Firefox GNOME theme](https://github.com/rafaelmardojai/firefox-gnome-theme) and [Thunderbird GNOME theme](https://github.com/rafaelmardojai/thunderbird-gnome-theme). <sup><sub>(If installed)</sub></sup>

> [!IMPORTANT]  
> **ISOs can be downloaded from our releases page [here](https://github.com/ublue-os/bazzite/releases), and a helpful install guide can be found [here](https://universal-blue.org/images/bazzite/installation/).**

To rebase an existing ostree system to the **desktop** release:

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite-gnome:latest
```

To rebase an existing ostree system to the **desktop with Nvidia drivers** release:

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite-gnome-nvidia:latest
```

> [!WARNING]  
> **Due to an upstream bug, Bazzite cannot be used on Steam Decks with 64GB eMMC storage at this time.**

To rebase an existing ostree system to the **Steam Deck/HTPC** release: 

```bash
rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/bazzite-deck-gnome:latest
```

## Why

Bazzite started as a project to resolve some of the issues that plague SteamOS, mainly out of date packages (despite an Arch base) and the lack of a functional package manager.

Despite this project also being image-based, you are able to install any Fedora package straight from the command line. These packages will persist across updates <sub><sup>(So go ahead and install that obscure VPN software you spent an hour trying to get working in SteamOS)</sup></sub>. Additionally, Bazzite is updated multiple times a week with packages from upstream Fedora, giving you the best possible performance and latest features - all on a stable base.

Bazzite ships with the latest Linux kernel and SELinux enabled by default with full support for secure boot <sub><sup>(Run `ujust enroll-secure-boot-key` and enter the password `ublue-os` if prompted to enroll our key)</sup></sub> and disk encryption, making this a sensible solution for general computing. <sup><sub>(Yes, you can print from Bazzite)</sub></sup>

Check out the [FAQ](https://universal-blue.org/images/bazzite/FAQ/) for other topics surrounding the project.

## Showcase

![KDE Vapor Theme](/repo_content/desktop1.png?raw=true "KDE Vapor Theme")
![KDE VGUI2 Theme](/repo_content/desktop2.png?raw=true "KDE VGUI2 Theme")
![Steam Game Mode](/repo_content/gamemode.png?raw=true "Steam Game Mode")
![Waydroid](/repo_content/waydroid.png?raw=true "Waydroid")
![Distrobox Terminals](/repo_content/distrobox.png?raw=true "Distrobox Terminals")
![GNOME Vapor Theme](/repo_content/gnome1.png?raw=true "GNOME Vapor Theme")
![GNOME VGUI2 Theme](/repo_content/gnome2.png?raw=true "GNOME VGUI2 Theme")

Check out our [newsletters](https://universal-blue.org/blog/category/bazzite/) that get published on a regular basis for updates on the project.

## Custom Packages

Ported SteamOS and ChimeraOS packages, among others used by Bazzite, are built on Copr in [bazzite](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/) and [bazzite-multilib](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite-multilib/).

|Package|Status|
|---|---|
|[discover-overlay](https://github.com/trigg/Discover)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/discover-overlay/status_image/last_build.png?)|
|ds-inhibit|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/ds-inhibit/status_image/last_build.png?)|
|duperemove|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/duperemove/status_image/last_build.png?)|
|[extest](https://github.com/Supreeeme/extest)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite-multilib/package/extest/status_image/last_build.png?)|
|gamescope|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite-multilib/package/gamescope/status_image/last_build.png?)|
|[gamescope-session-plus](https://github.com/ChimeraOS/gamescope-session)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gamescope-session-plus/status_image/last_build.png?)|
|[gamescope-session-steam](https://github.com/ChimeraOS/gamescope-session-steam)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gamescope-session-steam/status_image/last_build.png?)|
|[gnome-randr-rust](https://github.com/maxwellainatchi/gnome-randr-rust)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gnome-randr-rust/status_image/last_build.png?)|
|gnome-shell-extension-bazzite-menu|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gnome-shell-extension-bazzite-menu/status_image/last_build.png?)|
|[gnome-shell-extension-caribou-blocker](https://extensions.gnome.org/extension/1326/block-caribou/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gnome-shell-extension-caribou-blocker/status_image/last_build.png?)|
|[gnome-shell-extension-hanabi](https://github.com/jeffshee/gnome-ext-hanabi)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gnome-shell-extension-hanabi/status_image/last_build.png?)|
|[gnome-shell-extension-compiz-windows-effect](https://github.com/hermes83/compiz-windows-effect)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/gnome-shell-extension-compiz-windows-effect/status_image/last_build.png?)|
|jupiter-fan-control|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/jupiter-fan-control/status_image/last_build.png?)|
|jupiter-hw-support-[btrfs](https://gitlab.com/popsulfr/steamos-btrfs)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/jupiter-hw-support-btrfs/status_image/last_build.png?)|
|[mangohud](https://github.com/flightlessmango/MangoHud)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite-multilib/package/mangohud/status_image/last_build.png?)|
|mesa|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite-multilib/package/mesa/status_image/last_build.png?)|
|powerbuttond|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/powerbuttond/status_image/last_build.png?)|
|[python3-hid](https://github.com/apmorton/pyhidapi)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/python3-hid/status_image/last_build.png?)|
|rmlint|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/rmlint/status_image/last_build.png?)|
|[ryzenadj](https://github.com/FlyGoat/RyzenAdj)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/ryzenadj/status_image/last_build.png?)|
|[sddm-sugar-steamOS](https://github.com/JiayuanWen/sddm-sugar-steamOS)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/sddm-sugar-steamOS/status_image/last_build.png?)|
|[sdgyrodsu](https://github.com/kmicki/SteamDeckGyroDSU)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/sdgyrodsu/status_image/last_build.png?)|
|steamdeck-gnome-presets|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/steamdeck-gnome-presets/status_image/last_build.png?)|
|steamdeck-kde-presets|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/steamdeck-kde-presets/status_image/last_build.png?)|
|steamdeck-kde-presets-desktop|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/steamdeck-kde-presets-desktop/status_image/last_build.png?)|
|steam_notif_daemon|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/steam_notif_daemon/status_image/last_build.png?)|
|udisks2|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/udisks2/status_image/last_build.png?)|
|vpower|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/bazzite/package/vpower/status_image/last_build.png?)|

Additionally, the following packages are used from other Copr repos:

|Package|Status|
|---|---|
|[gcadapter_oc-kmod](https://copr.fedorainfracloud.org/coprs/ublue-os/akmods/)|![Build Status](https://copr.fedorainfracloud.org/coprs/ublue-os/akmods/package/gcadapter_oc-kmod/status_image/last_build.png?)|
|[gnome-vrr](https://copr.fedorainfracloud.org/coprs/kylegospo/gnome-vrr/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/gnome-vrr/package/mutter/status_image/last_build.png?)|
|[hl2linux-selinux](https://copr.fedorainfracloud.org/coprs/kylegospo/hl2linux-selinux/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/hl2linux-selinux/package/hl2linux-selinux/status_image/last_build.png?)|
|[latencyflex-vulkan-layer](https://copr.fedorainfracloud.org/coprs/kylegospo/LatencyFleX/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/LatencyFleX/package/latencyflex-vulkan-layer/status_image/last_build.png?)|
|[noise-suppression-for-voice](https://copr.fedorainfracloud.org/coprs/ycollet/audinux/)|![Build Status](https://copr.fedorainfracloud.org/coprs/ycollet/audinux/package/noise-suppression-for-voice/status_image/last_build.png?)|
|[obs-vkcapture](https://copr.fedorainfracloud.org/coprs/kylegospo/obs-vkcapture/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/obs-vkcapture/package/obs-vkcapture/status_image/last_build.png?)|
|[openrgb-kmod](https://copr.fedorainfracloud.org/coprs/ublue-os/akmods/)|![Build Status](https://copr.fedorainfracloud.org/coprs/ublue-os/akmods/package/openrgb-kmod/status_image/last_build.png?)|
|[rom-properties](https://copr.fedorainfracloud.org/coprs/kylegospo/rom-properties/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/rom-properties/package/rom-properties/status_image/last_build.png?)|
|[steamdeck-kmod](https://copr.fedorainfracloud.org/coprs/ublue-os/akmods/)|![Build Status](https://copr.fedorainfracloud.org/coprs/ublue-os/akmods/package/jupiter-kmod/status_image/last_build.png?)|
|[system76-scheduler](https://copr.fedorainfracloud.org/coprs/kylegospo/system76-scheduler/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/system76-scheduler/package/system76-scheduler/status_image/last_build.png?)|
|[wallpaper-engine-kde-plugin](https://copr.fedorainfracloud.org/coprs/kylegospo/wallpaper-engine-kde-plugin/)|![Build Status](https://copr.fedorainfracloud.org/coprs/kylegospo/wallpaper-engine-kde-plugin/package/wallpaper-engine-kde-plugin/status_image/last_build.png?)|

## Verification

These images are signed with sigstore's [cosign](https://docs.sigstore.dev/cosign/overview/). You can verify the signature by downloading the `cosign.pub` key from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/ublue-os/bazzite
```

### Contributor Metrics

![Bazzite](https://repobeats.axiom.co/api/embed/86b500d79c613015ad16f56df76c8e13f3fd98ae.svg "Repobeats analytics image")

## Special Thanks

Bazzite is a community effort and wouldn't exist without everyone's support. Below are some of the people who've helped us along the way:

- [rei0260](https://discord.com/users/rei0260) - For creating our logo and overall branding.
- [evlaV](https://gitlab.com/evlaV) - For making Valve's code available and for being [this person](https://xkcd.com/2347/).
- [ChimeraOS](https://chimeraos.org/) - For gamescope-session and for valuable support along the way.
- [Jovian-NixOS](https://github.com/Jovian-Experiments) - For supporting us with technical issues and for creating a similar project. Seriously, go check it out. It's our Nix-based cousin.
- [Steam Deck Homebrew](https://deckbrew.xyz) - For choosing to support distributions other than SteamOS despite the extra work, and a special thanks to [PartyWumpus](https://github.com/PartyWumpus) for getting Decky Loader working with SELinux for us.
- [cyrv6737](https://github.com/cyrv6737) - For the initial inspiration and the base that became bazzite-arch.

## Build Your Own

Bazzite is built entirely in GitHub and creating your own custom version of it is as easy as forking this repository, adding a private signing key, and enabling GitHub actions.

[Familiarize yourself](https://docs.github.com/en/actions/security-guides/encrypted-secrets) on keeping secrets in github. You'll need to [generate a new keypair](https://docs.sigstore.dev/cosign/overview/) with cosign. The public key can be in your public repo <sub><sup>(Your users need it to check the signatures)</sup></sub>, and you can paste the private key in `Settings -> Secrets -> Actions` with the name `SIGNING_SECRET`.

We also ship a config for the popular [pull app](https://github.com/apps/pull) if you'd like to keep your fork in sync with upstream. Enable this app on your repo to keep track of Bazzite changes while also making your own modifications.

## Join The Community

You can find us on the [Universal Blue Discord](https://discord.gg/f8MUghG5PB).

You can also discuss on our [Github Discussions](https://github.com/orgs/ublue-os/discussions/categories/bazzite) for any new features or issues you're experiencing with Bazzite.

<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM169.8 165.3c7.9-22.3 29.1-37.3 52.8-37.3h58.3c34.9 0 63.1 28.3 63.1 63.1c0 22.6-12.1 43.5-31.7 54.8L280 264.4c-.2 13-10.9 23.6-24 23.6c-13.3 0-24-10.7-24-24V250.5c0-8.6 4.6-16.5 12.1-20.8l44.3-25.4c4.7-2.7 7.6-7.7 7.6-13.1c0-8.4-6.8-15.1-15.1-15.1H222.6c-3.4 0-6.4 2.1-7.5 5.3l-.4 1.2c-4.4 12.5-18.2 19-30.6 14.6s-19-18.2-14.6-30.6l.4-1.2zM224 352a32 32 0 1 1 64 0 32 32 0 1 1 -64 0z"/></svg>](https://universal-blue.org/images/bazzite/FAQ/)
