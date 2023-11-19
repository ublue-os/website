# Frequently Asked Questions

This is a very lengthy FAQ that attempts to cover several different topics surrounding Bazzite. If you are looking for something specific then please use the table of contents because this is a really long page that tries to cover all of the Bazzite images.

## General FAQ

### Why is it called Bazzite?
Fedora Linux's image-based desktops are usually named after [minerals](https://fedoraproject.org/kinoite/) or [flowers](https://fedoraproject.org/sericea/).  Bazzite is a mineral that is known for being strong, lightweight, and is colored [blue](https://universal-blue.org/).

### What image do I use?
Images are split up between **2 types of images**: 

#### Desktop
_AMD/Intel Desktop Images_: Steam and other gaming utilities are layered to the image.  **No "Game Mode" on these images**, but is similar to SteamOS's "Desktop Mode" from an end user point of view.  

_Nvidia Desktop Images_: Very similar to their AMD/Intel desktop counterparts, but preinstalls Nvidia's proprietary graphic drivers to the image, and there are features like Waydroid out of the box.

#### Steam Deck / HTPC / Handheld PC
Mimics SteamOS with "Game Mode" with most of the features fully functional.  Can be used on most devices using a modern AMD/Intel GPU.  **Nvidia is currently not supported.**

#### Desktop Environments & Specific Hardware

All of the images also come with the choice of using [KDE Plasma](https://kde.org/plasma-desktop/) or [GNOME](https://www.gnome.org/) for the desktop environment and made with specific hardware in mind.

There is more information about this on the [installation documentation](/images/bazzite/installation/). 

### I am new to Linux gaming.  Where do I start?
Welcome!  We have a gaming starter guide [here](/images/bazzite/gaming_guide).  

The Steam Deck/HTPC images should be a very similar to SteamOS.

### SteamOS is based on Arch Linux, so why use Fedora Linux as the base? 
SteamOS is based on Arch Linux, but the base packages and drivers get updates at a much slower pace than using vanilla Arch and updating yourself. Bazzite will follow Fedora's updates which means it will always be ahead of SteamOS in terms of newer software and drivers.  Also Fedora Linux currently is the only Linux distribution that supports OCI custom images that this whole project is built around.  The end user typically shouldn't notice too much of a difference between Bazzite and SteamOS in terms of losing features. 

### How does Bazzite differ from other Linux distributions?
Like SteamOS, Bazzite makes use of read-only root files for stability purposes.

Bazzite is Fedora Linux built with [libostree](https://ostreedev.github.io/ostree/) which has advantages such as:

* Atomic updates for system and applications.
* Containerized applications that do not interfere with your host system.
* Overlay RPM packages to the host that survive upgrades.
* Smooth upgrade process from major Fedora point releases.
* Low risk of an unbootable or broken system. 
* Rollback system updates if necessary and the ability pin your current deployment as a backup "save state."

Check out [Fedora Silverblue](https://fedoraproject.org/silverblue/) and [Universal Blue homepage](https://universal-blue.org) for more information on what the libostree project is capable of.

### Is this another fringe distro?
Bazzite is not a distribution in the same sense that other Fedora-based distributions are.  These images are [Fedora Kinoite (KDE)](https://fedoraproject.org/kinoite/) and [Fedora Silverblue (GNOME)](https://fedoraproject.org/silverblue/) with a recipe on top of it.  This is a new "container-native" method that Fedora has been testing, and we are taking full advantage of this.  We are utilizing the [Open Container Initiative](https://opencontainers.org/) to create these images, and are simply adding packages, services, kernel modules, etc. to existing Fedora images.  Bazzite takes from the "main" Universal Blue Fedora image and adds to it.  Bazzite's goal is Fedora Linux, but provide a great gaming experience out of the box.

Unlike traditional Linux distributions, much of the maintenance and security updates are done upstream by Fedora and Universal Blue while Bazzite only has to focus on the gaming aspects of it.  A hypothetical scenario where everyone involved with Bazzite could stop maintaining the project at once and it will still continue to receive updates directly from Fedora.  Check out the [mission statement](/mission) and [documentation](https://universal-blue.org/introduction/) for more information.

### What is Wayland and X11?
In short, Wayland and X11 (also known as Xorg or the X Window System) are windowing systems for desktop Linux.

* Wayland is the default for most of the images and the recommended option for Bazzite.
* X11 is a legacy windowing system. While we recommend to stick with Wayland, there may be scenarios where X11 would have to be used. Nvidia GPUs may have issues with Wayland, so X11 is the default for the Nvidia images.

You can swap between the two in the login screen for desktop images, and enter `ujust _toggle_wayland` in a host terminal for Steam Deck/HTPC/Handheld PC images.

### What are some of the unique applications that Bazzite uses?
- [Bazzite Portal, also known as YAFTI](https://github.com/ublue-os/yafti/), acts as both a first-boot utility and general software configuration and installation tool.
- [Just](https://github.com/casey/just) is for executing custom commands based on recipes.  Type `ujust` in a host terminal to see what commands are available.  See some example commands [here](/guide/just/).
- [Fleek](https://getfleek.dev/) is a [Nix](https://search.nixos.org/packages) package manager wrapper and `$HOME` manager using YAML.
- [OBS-Portable OCI Image](https://github.com/ublue-os/obs-studio-portable) is the universal installation method of the [OBS-Portable](https://github.com/wimpysworld/obs-studio-portable) which aims to be OBS Studio with codecs and several popular plugins preinstalled, and as the name implies it's a portable application too.


### Steam is not launching on my desktop with hybrid graphics, what should I do?
This would be out of scope for our project due to it being an issue currently with Steam itself and not Bazzite, but we had enough support tickets surrounding it that we are including the fix in our FAQ.

Recently, Steam breaks if you have hybrid graphics in your PC.  The solution is simply locating the .desktop file for Steam (non-Flatpak versions are located in: `~/.local/share/applications/`) and opening it with a text editor (Kate, Text Editor, etc.), and adding this to the last line under `[Desktop Entry]`:
```bash
PrefersNonDefaultGPU=false
X-KDE-RunOnDiscreteGpu=true
```
Save the file.  Steam should now launch.

Read more about this issue [here](https://github.com/ValveSoftware/steam-for-linux/issues/9940).

###  I am experiencing a bug or want to request a feature! Help!
In order to troubleshoot the issue properly, you should add a log or terminal output of the issue.  

**Example 1:** For a game running on Steam through Proton, go to the game's properties and type `PROTON_LOG=1 %command%` in the launch options section.  Play the game and the log should appear by the appid in your `Home` directory, and make sure to attach that to the issue you have opened.

**Example 2**: For a Flatpak application that has issues, get the Flatpak package name of all installed applications by entering `flatpak list` (you may need to readjust the terminal window to get the package name to fit beforehand.)  After you got the name, enter `flatpak run <flatpak.package.name>` and a console output will appear.  Copy and paste into a text file, save it, and attach it.

Explain your issue or proposal in our [issue tracker](https://github.com/ublue-os/bazzite/issues) or [Github Discussions Page](https://github.com/orgs/ublue-os/discussions/categories/bazzite).

It's always a good idea to try and manually update your system by entering in a host terminal: `rpm-ostree update` and `ublue-update`, then waiting for the system to get the latest upgrades, and rebooting to see if the issue still persists.

One of the goals of this project is to have the convenience of never worrying about having to reinstall your operating system.  However, all of this is new, and anything can explode horribly if you try hard enough.  When the worst-case scenario appears and the only solution is to reinstall Bazzite, then please backup your personal files in your `Home` directory as well as any drives connected to your device.  Application data for Flatpaks, which is anything installed from Discover or GNOME Software, are stored in your Home directory under `~/.var/app/`.  Make sure you have hidden files enabled in the file manager to see all of your files.

### I would like to contribute to Bazzite.  Where do I start?
Thank you for being so eager to contribute to the project!  Bazzite has a [suggestions thread](https://github.com/orgs/ublue-os/discussions/246) where you can suggest any feedback to the project.  If you want to develop or provide documentation for Bazzite, then read the contributing [guide](/images/bazzite/CONTRIBUTING).  This guide also links to our roadmap for future plans with the project.

## Installation

### How do I install Bazzite on my device?
Follow this [guide](/images/bazzite/installation/).

### Can I dual-boot Bazzite with Windows?
**Short answer: It's unsupported, but can work especially if Windows is on a different drive.**

Dual-booting Bazzite with Windows works, but it is recommended if the both operating systems are on **a separate drive and have Windows already installed first**.  

If you do not have multiple drives, then there is an advanced method that requires manual partitioning (which is unsupported if you run into any issues here.)

1.  Shrink partitions.
2.  Write ISO to USB drive.
3.  Boot into ISO via BIOS.
4.  Use installer - for partitioning select "custom" or "advanced custom" to be absolutely sure.
5.  Create partitions and devices
   
    ```
    manual partitioning scheme:

    mount point: /boot/efi  
    format:      vfat    
    size:        300MB  
    (optional: use existing system efi partition)

    mount point: /boot
    format:      ext4
    size:        1GB

    mount point:
    format: btrfs
    size: [max]

    mount point: /
    format:      btrfs (subvolume)

    mount point: /var
    format:      btrfs (subvolume)

    mount point: /var/home
    format:      btrfs (subvolume)
    ```
6. Boot into Bazzite and complete the Bazzite Portal.
7. Reboot
8. Should have both OSes on the same drive

### I am having issues installing Bazzite on my hardware! What's going on?
OCI images are very new and the Fedora installer, Anaconda, has some issues with this.  If you have skills in [Lorax](https://weldr.io/lorax/f28-branch/lorax.html) and the [Anaconda installer](https://www.fedoraproject.org/wiki/Anaconda), please help by contributing!  This is one of the most difficult hurdles that Bazzite and the Universal Blue project face.  We are dependent on upstream to resolve the issues currently.

**Here are the main installer issues and their workarounds:**

#### Blank screen on boot

This is currently a known [issue](https://github.com/ublue-os/bazzite/issues/109).  There is a [workaround](https://github.com/ublue-os/bazzite/issues/109#issuecomment-1691090533) that requires either the stock [Fedora Kinoite](https://fedoraproject.org/kinoite/) ISO and rebase to Bazzite from the terminal after installation.  The installer is the same one we use for Bazzite, and all of the data from the installer will carry over to Bazzite.

**Rebasing from stock Fedora Kinoite image method**:

      - Download and install either Fedora Kinoite (KDE Plasma) or Fedora Silverblue (GNOME).
      - When you get to the desktop, open the terminal and enter the rebase command to an unsigned image.
      - See the Bazzite [README](https://github.com/ublue-os/bazzite#readme) to see the rebase commands for each image.
      - When it has finished, reboot your PC and you should now be on the Bazzite image you chose.
      - The image will be signed during Bazzite Portal completion.

**Other methods that may work:**

- Remove the `rd.live.check` line from the boot parameters in grub. Press <kbd>E</kbd> on a physical keyboard when you see the boot option.  After removing that line, press <kbd>CTRL</kbd>+<kbd>X</kbd> to save.  It should boot now, and this line skipped the media verification which is the default behavior in the installer.

- Booting the bootable media from UEFI BIOS if possible.

- Installing with basic graphics mode in the installer

- [Advanced guide](https://sharing.io/deck.html) that is very command-line heavy to install Bazzite.

Keep in mind we do **not** support booting using Ventoy.

!!! warning

    Keep in mind that the Steam Deck will not scale properly with the stock Fedora Silverblue/Kinoite installer, and the buttons on the bottom of the screen will be cut off.  This will require the use of the <kbd>TAB</kbd> key on your keyboard to navigate the installer blindly.

#### Error occured while installing the payload (Installer GUI Error)
Make sure you are connected to the internet if you are using an online ISO.  If you are, and there is still an issue, there might be an issue with your network adapter and Linux.  It is recommended to use a wired connection if you can, especially if this occurs after connecting to a wireless network.  If you are confident that the connection is stable and your network adapter works on Linux, then try the Fedora Kinoite rebase method above.

## Installing and Managing Software

### How do I install additional software?

#### Flatpak
Flatpak is the default method of installing applications on Bazzite.  It is a universal containerized package format that tries to sandbox applications through flexible permissions that the application has access to on your system.

Typically it is recommended to use Flatpak for most software if possible.  These can be installed via the software center that is preinstalled like *Discover* or *GNOME Software*.  Take a look at the [selection](https://flathub.org/apps/collection/popular/1).

Manage Flatpaks with Flatseal and Warehouse which are both preinstalled.

#### AppImage
AppImage is a universal package method that attempts to bundle every single dependency that an application needs into one portable file.

AppImages can be installed by downloading any file with an `.AppImage` extension.  These are usually found on a project's website, [AppImage Hub](https://www.appimagehub.com/) or if you install [AppImage Pool](https://flathub.org/apps/io.github.prateekmedia.appimagepool). Then giving the AppImage application executable permssions in the file's properties so the application can run properly.

Manage AppImages with the Gear Lever application that is preinstalled.

!!! Note
    AppImages are not supported in other Universal Blue images (like Bluefin.)

#### Distrobox
Distrobox containers are running subsystems of other popular Linux distributions with access to their package managers and their package formats (ex: `.deb`/`.rpm`) 

Distrobox containers can be made with the host terminal following this [documentation](https://github.com/89luca89/distrobox/blob/main/docs/usage/distrobox-create.md). 

There are pre-made `ujust` commands to create a container of operating systems.  Ex: `ujust distrobox-fedora` to create a Fedora Linux Distrobox container to have access to `dnf`.  Keep in mind that this is still a container, so dependencies and libraries from anything you install are not part of your host.  

[Full list of other distributions that work in Distrobox](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros).

#### Nix
Nix is a cross-platform and declarative package manager that can be described as an "atomic" package manager.  There is a learning curve however, but Bazzite tries to keep it simple with the integration of [Fleek](https://github.com/ublue-os/fleek).

If you opted to use Nix packages at the first boot, then you can use the Nix package manager.  More information on how to use the Nix package manager [here](https://zero-to-nix.com/).

#### Brew
Brew is a popular package manager that is intended as a community-driven package manager for macOS, which also has a Linux port for it.  It attempts to install packages in their own directories and prefixes keeping your directories clean.

Brew is available by entering `ujust install-brew` and `ujust install-brew-to-shell`.  Read the [official documentation](https://docs.brew.sh/Homebrew-on-Linux) on how to use it.

#### Bash Scripts
Some applications require you to execute a Bash script (`.sh` extension).  Like AppImages, go into the script's file properties and give it executable permissions, and run it in your host terminal.

#### rpm-ostree
Obtain Fedora Linux packages like you typically would with their package manager.  However, it is highly recommended to only use this command as the last resort especially if the package can be obtained through the above methods.  Layering packages to your image is mostly intended for system-level packages.

Fedora has [documentation](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/rpm-ostree/) on rpm-ostree.  The most common commands are `rpm-ostree install <package>` and `rpm-ostree uninstall <package>`.  Each package layered will be installed on the next reboot. 

### How do I run Windows applications?
* Lutris (preinstalled) for non-Steam video games.
* [Bottles](https://flathub.org/apps/com.usebottles.bottles) for general-purpose applications or as an alternative to Lutris.
* [Heroic](https://flathub.org/apps/com.heroicgameslauncher.hgl) for Epic, GOG, and Amazon Games Launcher.
* [itch](https://flathub.org/apps/io.itch.itch) for games on itch.io.  Also comes preinstalled with a Wine runner.

### How do I run Android applications?
Follow the [Waydroid guide](/images/bazzite/waydroid/).

### How do I view all the system packages installed on Bazzite?
Open a host terminal and enter `rpm -qa` and an output of every system package will be listed.

## Updates, Rollbacks, and Rebasing

### How do updates work?

#### Desktop images (*bazzite*, *bazzite-nvidia*, *bazzite-gnome*, and *bazzite-gnome-nvidia*, etc.)
System updates happen automatically daily.  They will be downloaded in the background and will apply on shutdown or a reboot.  These system updates are NOT forced.  Bazzite downloads the latest patches in the background and they will be applied as soon as you shut down.  The next reboot will contain the newest changes.   No need for worrying about manually upgrading your system.

Flatpak applications (installed from *Discover* or *GNOME Software*) also update twice a day automatically.  Distrobox containers are also automatically updated too.

You can force an update to the whole system (base packages, applications, and containers) at any time by opening your host terminal and entering `ublue-update` then reboot your device after it has finished.

#### Steam Deck and HTPC images (*bazzite-deck* and *bazzite-deck-gnome*, etc.)
Similar to SteamOS, updates are handled by Steam.  In Game Mode, go to Settings > System > click "Apply"

Alternatively, you can open a host terminal and enter `ublue-update`, then reboot your device after it has finished.  Updates upgrade your system, Flatpak applications, and distrobox containers all at once.

### How does updating to a new Fedora point release work?
Your system should automatically update when our new builds based on that new point release are ready on Desktop images, and Steam Deck images should update to the new release when you update in Game Mode.  Bazzite usually aims for the same day when the new Fedora Linux version releases.  

Advanced users can test early builds by [rebasing](/images/bazzite/FAQ/#i-think-i-installed-the-wrong-bazzite-image-do-i-have-to-reinstall) to a beta image when avaliable at their own risk.

### Do I have to reboot after every system update or layering a package (with rpm-ostree)? 
No, but the upgrade won't apply until the next reboot and the package you layered to the image through `rpm-ostree` won't be there either.  You can attempt to layer package without rebooting with `rpm-ostree install --apply-live <package>` but sometimes this still requires a reboot depending on the package(s) you installed.

### How do I rollback a system update?
You can rollback in the GRUB menu by choosing the previous boot entry. Your personal files will NOT be affected by this, and you can still update to the newest builds on older system builds.

!!! Note
    Steam Deck/HTPC/Handheld PC images do not show the GRUB menu by default, so when you boot up your device press "B" on the Steam Deck or <kbd>Esc</kbd> on a physical keyboard for it to appear.

You can pin your current deployment with `sudo ostree admin pin 0` in a host terminal for a backup save state of your current deployment.  

**For advanced users**: We also offer specific builds from the last 90 days that you can rebase to, but you will have to rebase back to `:latest` once you want to upgrade.  If you want to rollback within the 90 days of builds to a specific build, enter: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite-deck:YEARMONTHDAY` (ex:20231031) for October 31, 2023.

Read Fedora's official [documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/updates-upgrades-rollbacks/#rolling-back) on the topic of rolling back.

### How do I disable automatic updates for system and applications?

!!! warning

    Disabling automatic updates is an unsupported configuration.

If you are disabling this for performance concerns, there is no need.  There are checks in place to prevent updates when the system is under heavy use, including gaming.

Open a host terminal and enter: `systemctl disable ublue-update`.

**This is not recommended.** 

### I think I installed the wrong Bazzite image!  Do I have to reinstall?
No.  If you installed the wrong Bazzite image or want to use another image then you can switch to another Bazzite or any other Universal Blue image without losing any of user data by **rebasing**.  Enter the command in a host terminal found on this [page](/images/) for whatever image you're looking for, but make sure you're using `:latest`.  After it is finished rebasing, reboot your system to be in the new image.

You can also rebase to a stock Fedora imaged-based desktop image by entering in a host terminal `ostree remote refs fedora` to see a list of available Fedora images that you can rebase to.  Afterwards, enter `rpm-ostree rebase <image>` and wait for it to install the image then reboot.

!!! note

    Rebasing from KDE Plasma images to GNOME images may have major issues.  Rebasing from GNOME to KDE Plasma is usually fine however.
    
### How do I change the Bazzite branch? (Latest, Testing, and Unstable)

There are 3 branches you can switch to:

- Latest (default, stable)  
- Testing
- Unstable (Not recommended)

Steam Deck/HTPC/Handheld PCs can switch branches inside of Settings > System > OS Update Channel.

Other images, or a manual command-line method is adding `:testing` or `:unstable` to the end of the rebase command for your Bazzite image.

**Ex**: `rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bazzite:testing` for the testing branch on a AMD/Intel desktop image.

### How do I disable update notifications for desktop images?

Open the directory `/etc/ublue-update/` and open `ublue-update.toml` with a text editor.

Change:
`dbus_notify = true` to `dbus_notify = false`

Notifications for updates are now suppressed.

## Steam Deck Images FAQ

###  How similar is Bazzite to SteamOS on Steam Deck hardware?
It should nearly be identical to the end user.  Bazzite Steam Deck images include the latest Gamescope and packages, which means we are always ahead of SteamOS in terms of Game Mode and Desktop Mode features.  The Quick Access Menu (Accessed with the <kbd>...</kbd> button) is functional for TDP, framerate caps, scaling, etc.  Performance should be on par or better than SteamOS, and every game SteamOS can play should play well on Bazzite.

Third-party software like Decky Loader, Emudeck, RetroDeck, etc. work and can be installed from the Bazzite Portal, but certain tools like CryoUtilities does not work.  If you want the swap functionality from CryoUtilities, then you can switch to using swap and adjust the size in the Bazzite Portal, but it is not recommended.  

Desktop Mode still has access to all of the applications in Discover that SteamOS has.  

**The only missing feature that SteamOS has over Bazzite currently is HDR support, but this should change once Fedora Linux supports it.**

### Does the Steam Deck image recieve BIOS updates like SteamOS?

**Yes it does**.  If a BIOS update is available then it will install when you update Bazzite normally.  If desired, there is a **command to disable BIOS updates at your own risk**: `ujust disable-bios-updates`.

### Why is the stock 64GB Steam Deck not supported on Bazzite?

It has filesystem corruptions.  You will have booting issues, freezes, and will not be able to update the image.  Upgrade the storage to resolve this if you feel comfortable doing so.

### Why do the Nvidia images not include Game Mode and Waydroid?
Nvidia's proprietary drivers currently do not work with any of this.  AMD and Intel have open source drivers on Linux and are usaully the far better option to use.  

Hopefully this changes in the future thanks to the upcoming [NVK](https://www.collabora.com/news-and-blog/news-and-events/introducing-nvk.html) project. Then most desktop Linux users would not have to bother with Nvidia's closed source driver philosophy and all of the downsides that come with that. 

###  I'm using the Steam Deck image on my HTPC, but there are games that force specific Steam Deck features I do not want like a specific controller layout.  Help?
Open the game's properties and under "LAUNCH OPTIONS", add: `SteamDeck=0 %command%` to force a game's "Steam Deck" features to be turned off.

![image](https://github.com/ublue-os/website/assets/121328689/9175f6b8-5a70-49fe-b270-fbc55e8510c0)

Currently, an example of a game where this is needed is Warframe.  Without this launch option, you cannot play Warframe on the Steam Deck images with a keyboard and mouse.

### On Steam Deck, Handheld PC, and HTPC images I am stuck updating at 99%, and the changelog is the same after every update.  What gives?
The update indicator is actually faked due to the limitations of Steam itself expecting the user to be on SteamOS for that progress bar to give any accurate information.  

There is a set schedule for that to stop showing the progress indicator after a certain time, but sometimes this fails.  If it's still at 99% and it's been an unrealistic amount of time, do not worry about it.  It most likely applied the updates to your system, flatpaks, and distrobox containers.  If you are still paranoid then go into Desktop Mode, open a host terminal, and enter: `ublue-update`, and if it there's no errors, you're good.  That is exactly the same method as updating in Game Mode.

As for the changelog, those are for SteamOS and not Bazzite.  Some of it may apply since we share a lot of the same packages, but regardless, it will always show SteamOS changelogs by Valve and has no relation to the updates for Bazzite.  Check our [newsletters](https://universal-blue.org/blog/category/bazzite/) for major changes and features. If you want to see the patch notes in real time, check the newest [commits](https://github.com/ublue-os/bazzite/commits/main) on Github.


<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite)

