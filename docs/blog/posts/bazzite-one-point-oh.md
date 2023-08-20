---
date: 2023-08-20
comments: true
authors: 
  - KyleGospo
  - EyeCantCU
links:
  - Bazzite: https://github.com/ublue-os/bazzite
  
---

# Bazzite 1.0

After 192 days of development we'd like to introduce Bazzite 1.0! Bazzite is a custom image of Fedora 38 designed to being the best in Linux gaming to your PCs, including the Steam Deck:

<figure markdown>
  ![Vapor](https://raw.githubusercontent.com/ublue-os/bazzite/main/repo_content/desktop1.png){ width="600" }
  <figcaption>KDE's Vapor Theme</figcaption>
</figure>

Bazzite is built from [ublue-os/main](https://github.com/ublue-os/main) and [ublue-os/nvidia](https://github.com/ublue-os/nvidia) using [Fedora](https://fedoraproject.org/) technology, which means expanded hardware support and built in drivers are included. 

<figure markdown>
  ![Game mode](https://raw.githubusercontent.com/ublue-os/bazzite/main/repo_content/gamemode.png){ width="600" }
  <figcaption>Steam Game Mode</figcaption>
</figure>

Additionally, Bazzite adds the following features:

## Bazzite

- Proprietary Nvidia drivers pre-installed.
- Full hardware accelerated codec support for H264 decoding.
- Full support for AMD's ROCM OpenCL/HIP run-times.
- [xpadneo](https://github.com/atar-axis/xpadneo) driver for wireless Xbox One controllers.
- Full support for [DisplayLink](https://www.synaptics.com/products/displaylink-graphics).
- Includes Valve's KDE themes from SteamOS.
- [LatencyFleX](https://github.com/ishitatsuyuki/LatencyFleX), [vkBasalt](https://github.com/DadSchoorse/vkBasalt), [MangoHud](https://github.com/flightlessmango/Mangohud), and [OBS VkCapture](https://github.com/nowrep/obs-vkcapture) installed and available by default
- Support for [Wallpaper Engine](https://www.wallpaperengine.io/en). <sub><sup>(Only on KDE)</sup></sub>
- [Distrobox](https://github.com/89luca89/distrobox) preinstalled with automatic updates for created containers.
- Automated `duperemove` services for reducing the disk space used by wine prefix contents.
- [System76-Scheduler](https://github.com/pop-os/system76-scheduler) preinstalled, providing automatic process priority tweaks to your focused application and keeping CPU time for background processes to a minimum.
- Customized System76-Scheduler config with additional rules and CFS parameters from [Linux-TKG](https://github.com/Frogging-Family/linux-tkg).
- Uses [Google's BBR TCP congestion control](https://github.com/google/bbr) by default.
- [Input Remapper](https://github.com/sezanzeb/input-remapper) preinstalled and enabled. <sub><sup>(Available but default-disabled on the Deck variant)</sup></sub>
- Helpful first-start installer provides an easy way to install numerous applications and tweaks, including installing [CoreCtrl](https://gitlab.com/corectrl/corectrl) and [GreenWithEnvy](https://gitlab.com/leinardi/gwe).
- [Nix](https://nixos.org/) package manager optionally available.
- [Waydroid](https://waydro.id/) preinstalled for running Android apps. Future releases will offer to set this up for you. <sub><sup>(Not available on Nvidia builds)</sup></sub>

![Waydroid](https://raw.githubusercontent.com/ublue-os/bazzite/main/repo_content/gamemode.png)

- [OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB) i2c-piix4 and i2c-nct6775 drivers for controlling RGB on certain motherboards.
- [GCAdapter_OC](https://github.com/hannesmann/gcadapter-oc-kmod) driver for overclocking Nintendo's Gamecube Controller Adapter to 1000hz polling.
- Out of the box support for [Wooting](https://wooting.io/) keyboards.

## Bazzite Desktop

The desktop release also features the following:

- Runs Steam and Lutris in a [custom Arch Linux OCI](https://github.com/ublue-os/bazzite-arch/) via Distrobox.
- Option to automatically launch Steam in Big Picture Mode on boot for HTPCs.

## Bazzite on Deck

The Steam Deck release also features the following:

- Directly boots to Gamemode matching SteamOS's behavior.
- **Automatic `duperemove` greatly trims the size of compatdata.**
- **Latest version of Mesa creates smaller shader caches and does not require them to prevent stutter.**
- **Able to be booted even if the drive is full.**
- Uses Wayland on the desktop with [full support for Steam input](https://github.com/Supreeeme/extest).
- Features ported versions of most SteamOS packages, including drivers, firmware updaters, and fan controllers [from the evlaV repository](https://gitlab.com/evlaV).
- Patched Mesa for proper framerate control from Gamescope.
- Comes with patches from [SteamOS BTRFS](https://gitlab.com/popsulfr/steamos-btrfs) for full BTRFS support for the SD card by default.
- Ships with a ported copy of [SDGyroDSU](https://github.com/kmicki/SteamDeckGyroDSU), enabled by default.
- Option to install [Decky Loader](https://github.com/SteamDeckHomebrew/decky-loader), [EmuDeck](https://www.emudeck.com/), and [ProtonUp-Qt](https://davidotek.github.io/protonup-qt/), among numerous other useful packages on installation.
- Custom update system allows for the OS, Flatpaks, and Distrobox images to be updated directly from the Gamemode UI.
- Built in support for Windows dual-boot thanks to Fedora's installation of GRUB being left intact.
- Update break something? Easily roll back to the previous version of Bazzite thanks to `rpm-ostree`'s rollback functionality. You can even select previous images at boot.
- Steam and Lutris preinstalled on the image as layered packages.
- Exclusively uses ZRAM by default with the option to switch back to a swap file and set a custom size if desired. <sub><sup>(1GB by default)</sup></sub>
- BFQ I/O scheduler to prevent I/O starvation when installing games or during background `duperemove` processes.
- TLS/SSL secured DNS and NTP by default. <sup><sub>(This is a handheld PC you're likely to use on random public networks after all)</sub></sup>
- Applies SteamOS's kernel parameters and enables `amd-pstate` by default.
- Default-disabled power-user features, including:
    - Service for low-risk undervolting of the Steam Deck via [RyzenAdj](https://github.com/FlyGoat/RyzenAdj), see `ryzenadj.service` and `/etc/default/ryzenadj`.
    - Service for limiting the max charge level of the battery, see `batterylimit.service` and `/etc/default/batterylimit`. <sup><sub>(Works even when the device is off)</sub></sup>
    - Built in support for display overclocking. For example, add `GAMESCOPE_OVERRIDE_REFRESH_RATE=40,70` to `/etc/environment`.
    - Ability to switch back to X11 on the desktop if desired by editing `/etc/default/desktop-wayland`.
    - 32GB RAM mod your Steam Deck? Enjoy double the maximum VRAM amount, automatically applied. <sup><sub>(Can you share your soldering skills?)</sub></sup>

## How to get it and current status

Start with [the documentation](https://universal-blue.org/images/bazzite/) and make sure you [follow the installation instructions carefully](https://universal-blue.org/images/bazzite/installation/)! The installation process is still considered incomplete, we're hoping to eventually migrate to the [new webui-based Anaconda installer](https://fedoramagazine.org/anaconda-web-ui-preview-image-now-public/) which will be much nicer for our use case. 

Like all Universal Blue images, Bazzite is using features that are on their way to Fedora, and are currently not considered stable. However with over 1.5 million image pulls over the last 9 months, we feel the model and method are proving to be reliable!

Download sizes are also currently less efficient than they should be. We're hoping that gamer interest in Fedora will bring in new ideas and contributors to help solve these issues.

## Join the crew

Bazzite is an open source project, contributions and feedback accepted! Check out the [Contributor's Guide](https://universal-blue.org/CONTRIBUTING) to get started and [join our Discord](https://discord.gg/WEu6BdFEtp).

We are especially in need of people with knowledge of the Anaconda installer so that we can make proper offline ISOs. 

## Special Thanks

Bazzite is a community effort and wouldn't exist without everyone's support. Below are some of the people who've helped us along the way:

- [evlaV](https://gitlab.com/evlaV) - For making Valve's code available and for being [this person](https://xkcd.com/2347/).
- [ChimeraOS](https://chimeraos.org/) - For gamescope-session and for valuable support along the way.
- [Jovian-NixOS](https://github.com/Jovian-Experiments) - For supporting us with technical issues and for creating a similar project. Seriously, go check it out. It's our Nix-based cousin.
- [Steam Deck Homebrew](https://deckbrew.xyz) - For choosing to support distributions other than SteamOS despite the extra work, and a special thanks to [PartyWumpus](https://github.com/PartyWumpus) for getting Decky Loader working with SELinux for us.
- [cyrv6737](https://github.com/cyrv6737) - For the initial inspiration and the base that became bazzite-arch.
