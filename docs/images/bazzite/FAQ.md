# FAQ

## Why is it called Bazzite?

Fedora's image-based variants are usually named after either [minerals](https://fedoraproject.org/kinoite/) or [flowers](https://fedoraproject.org/sericea/).

## How do I install Bazzite on my device?

Follow this [guide](/images/bazzite/installation/).

## Can I dual-boot?

Dual-boot is supported, but it is recommended if the other operating systems are on a separate drive.

## I am having issues installing Bazzite on my hardware! What's going on?

OCI images are very new and the Fedora installer, Anaconda, has some issues with this.  If you have skills in [Lorax](https://weldr.io/lorax/f28-branch/lorax.html) and the [Anaconda installer](https://www.fedoraproject.org/wiki/Anaconda), please help by contributing!  We are at a crossroads here because this is one of the most difficult hurdles that Bazzite and the Universal Blue project face.  We are essentially dependent on upstream to resolve the issues.

**Here are the main installer issues and their workarounds:**

### Black screen on boot and there are no logs

Remove the `rd.live.check` line from the boot parameters in grub. Press <kbd>E</kbd> on a physical keyboard when you see the boot option.  After removing that line, press <kbd>CTRL</kbd>+<kbd>X</kbd> to save.  It should boot now, and this line skipped the media verification which is the default behavior in the installer.

### Black screen with "dracut" mentioned in the logs

This is currently a known [issue](https://github.com/ublue-os/bazzite/issues/109).  There is a [workaround](https://github.com/ublue-os/bazzite/issues/109#issuecomment-1691090533) that requires either the stock Fedora Silverblue or Fedora Kinoite ISO and rebasing to Bazzite from there after installation.  
!!! warning

    Keep in mind that the Steam Deck will not scale properly with the installer, and the buttons on the bottom of the screen will be cut off.  This will require the use of the <kbd>TAB</kbd> key on your keyboard to navigate the installer blindly.

There is also two other **alternative** methods that may work:  
Installing with basic graphics mode in the installer or using this [advanced guide](https://sharing.io/deck.html) that is very command-line heavy.

Keep in mind we do **not** support booting using Ventoy.

### Error occured while installing the payload

Make sure you are connected to the internet if you are using an online ISO.  If you are, and there is still an issue, there might be an issue with your network adapter and Linux.  It is recommended to use a wired connection if you can, especially if this occurs after connecting to a wireless network.

## What image do I use?

Images are split up between **2 types of images**: 

### Desktop

_AMD/Intel Desktop Images_: Steam and other gaming utilities are installed in a [customized Arch Linux](https://github.com/ublue-os/bazzite-arch) [Distrobox container](https://github.com/89luca89/distrobox).  No "Game Mode" on these images, but is similar to SteamOS's "Desktop Mode" from an end user point of view.  

_Nvidia Desktop Images_: Very similar to their AMD/Intel desktop counterparts, but Steam and other gaming utilities are part of the image itself and are missing certain features like Waydroid.

### Steam Deck / HTPC / Handheld PC

Mimics SteamOS with "Game Mode" with most of the features you would expect from SteamOS.  Can be used on most devices using a modern AMD/Intel GPU.

### Desktop Environments & Specific Hardware

All of the images also come with the choice of using KDE Plasma or GNOME for the desktop environment and made with specific hardware in mind.

There is more information about this on the [installation documentation](/images/bazzite/installation/). 

## I am new to Linux gaming.  Where do I start?

We have a gaming starter guide [here](/images/bazzite/gaming_guide).  The Steam Deck image should be very similar to SteamOS to the end user.

## How do I install additional software?

### Flatpak

Typically it is recommended to use Flatpak for most software.  These can be installed via the software center that is preinstalled like *Discover* or *GNOME Software*.  Take a look at the [selection](https://flathub.org/apps/collection/popular/1).

### AppImage

AppImages can be installed by downloading any file with an `.AppImage` extension.  These are usually found on a project's website, [Appimage Hub](https://www.appimagehub.com/) or if you install [Appimage Pool](https://flathub.org/apps/io.github.prateekmedia.appimagepool). Then giving the AppImage application executable permssions in the file's properties so the application can run properly.

!!! Note
    AppImages are not supported in other Universal Blue images.

### Distrobox

Distrobox containers can be made with the host terminal following this [documentation](https://github.com/89luca89/distrobox/blob/main/docs/usage/distrobox-create.md). Keep in mind that `bazzite-arch` is a `distrobox` container that uses `pacman` as the package manager and can utilize the [AUR](https://aur.archlinux.org/).

You can use [other distributions](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros) inside their own containers.

### Nix

If you opted to use Nix packages at the first boot, then you can use the Nix package manager.  More information on that [here](https://zero-to-nix.com/).

### Brew

Brew is a popular package manager that was intended as a community-driven package manager for macOS.  There is also a Linux port for it.

Brew is available by entering `just install-brew` and `just install-brew-to-shell`.  Read the [official documentation](https://docs.brew.sh/Homebrew-on-Linux) on how to use it.

### rpm-ostree

Fedora has [documentation](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/rpm-ostree/) on rpm-ostree.  The most common command you will use is `rpm-ostree install <package>` to layer Fedora's RPM packages to the image.  After that has finished you will be required to reboot your system to use it.  However, it is highly recommended to only use this command as the last resort especially if the package can be obtained through the above methods.  Layering packages to your image using this is mostly intended for system-level packages, but any package available in Fedora can be layered using rpm-ostree.

## How do I run Windows applications?

* Lutris (preinstalled).
* [Bottles](https://flathub.org/apps/com.usebottles.bottles) for general-purpose applications or as an alternative to Lutris.
* [Heroic](https://flathub.org/apps/com.heroicgameslauncher.hgl) for Epic, GOG, and Amazon Games Launcher.

## How do I run Android applications?

Follow the [Waydroid guide](/images/bazzite/waydroid/).

## How do updates work?

### Desktop images (*bazzite*, *bazzite-nvidia*, *bazzite-gnome*, and *bazzite-gnome-nvidia*, etc.)

System updates happen automatically daily.  They will be downloaded in the background and will apply on shutdown or a reboot.  These system updates are NOT forced.  Bazzite downloads the latest patches in the background and they will be applied as soon as you shut down.  The next reboot will contain the newest changes.   No need for worrying about manually upgrading your system.

Flatpak applications (installed from *Discover* or *GNOME Software*) also update twice a day automatically.  Distrobox containers are also automatically updated too.

You can force an update to the whole system (base packages, applications, and containers) at any time by opening your host terminal and entering `ublue-update` then reboot your device after it has finished.

### Steam Deck and HTPC images (*bazzite-deck* and *bazzite-deck-gnome*, etc.)

Similar to SteamOS, updates are handled by Steam.  In Game Mode, go to Settings > System > click "Apply"

Alternatively, you can open a host terminal and enter `ublue-update`, then reboot your device after it has finished.  Updates upgrade your system, Flatpak applications, and distrobox containers all at once.

## How does updating to a new Fedora point release work?

Your system should automatically update when our new builds based on that new point release are ready on Desktop images, and Steam Deck images should update to the new release when you update in Game Mode.  Bazzite usually aims for the same day when the new Fedora releases.  Advanced users can test early builds by [rebasing](/images/bazzite/FAQ/#i-think-i-installed-the-wrong-bazzite-image-do-i-have-to-reinstall) to a beta image when avaliable at their own risk.

## Do I have to reboot after every system update or layering a package?

No, but update won't apply until shutdown.  You can attempt to layer package(s) without rebooting with `rpm-ostree install --apply-live <package>` however sometimes this still requires a reboot depending on the package(s) you installed.

## How do I rollback a system update?

Read Fedora's official [documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/updates-upgrades-rollbacks/#rolling-back) on this.  You can pin your current deployment with `sudo ostree admin pin 0` in a host terminal.  You can also rollback in the GRUB menu by choosing the previous boot entry. Your personal files will NOT be affected by this, and you can still update to the newest builds on older system builds.

!!! Note
    Steam Deck/HTPC/Handheld PC images do not show the GRUB menu by default, so when you boot up your device press "B" on the Steam Deck or <kbd>Esc</kbd> on a physical keyboard for it to appear.


## How do I disable automatic updates for system, Flatpaks, and Distrobox containers?

!!! warning

    Disabling automatic updates is an unsupported configuration.

If you are disabling this for performance concerns, there is no need.  There are checks in place to prevent updates when the system is under heavy use, including gaming.

Open a host terminal and enter: `systemctl disable ublue-update`.

**This is not recommended.** 

## How do I view all the system packages installed on Bazzite?

Open a host terminal and enter `rpm -qa` and an output of every system package will be listed.

### Now how do I remove a system package from the image?

!!! warning

    Removing packages that were preinstalled is an unsupported configuration.

Open a host terminal and enter `rpm-ostree override remove <package>` and reboot.  This will remove the package from the image.

**This is not recommended!**

However, if you installed a package via rpm-ostree and want to remove it from the image, then enter `rpm-ostree uninstall <package>` and reboot.  Unlike removing packages that came preinstalled with Bazzite, there isn't consequences to doing this.

## SteamOS is based on Arch Linux, so why use Fedora as the base? 

SteamOS is based on Arch Linux, but the base packages and drivers get updates at a much slower pace than using vanilla Arch and updating yourself. Bazzite will follow Fedora's updates which means it will always be ahead of SteamOS in terms of newer software and drivers.  Also Fedora currently is the only Linux distribution that supports OCI custom images that this whole project is built around.  The end user typically shouldn't notice too much of a difference between Bazzite and SteamOS. 

## How does Bazzite differ from other Linux distributions?

Like SteamOS, Bazzite makes use of read-only root files for stability purposes.

Bazzite is built off of desktop versions of Fedora built with [libostree](https://ostreedev.github.io/ostree/) which has advantages such as:

* Automatic and atomic updates for system and applications.
* Containerized applications which means dependency conflicts should not be a problem.
* Overlay system packages to the host so they survive updates.
* Smooth upgrade process from major Fedora point releases.
* Very little risk of an unbootable or broken system.
* Rollback system updates and pin your current deployment.

Check out the [Universal Blue homepage](https://universal-blue.org) for more information.

## Is this another fringe distro?

Bazzite is not a distribution in the same sense that other Fedora-based distributions are.  These images are [Fedora Kinoite (KDE)](https://fedoraproject.org/kinoite/) and [Fedora Silverblue (GNOME)](https://fedoraproject.org/silverblue/) with a recipe on top of it.  This is a new "container-native" method that Fedora has been testing, and we are taking full advantage of this.  We are utilizing the [Open Container Initiative](https://opencontainers.org/) to create these images, and are simply adding packages, services, kernel modules, etc. to existing Fedora images.  Bazzite takes from the "main" Universal Blue Fedora image and adds to it.  Bazzite's goal is Fedora Linux, but provide a great gaming experience out of the box.

Unlike traditional Linux distributions, much of the maintenance and security updates are done upstream by Fedora and Universal Blue while Bazzite only has to focus on the gaming aspects of it.  A hypothetical scenario where everyone involved with Bazzite could stop maintaining the project at once and it will still continue to receive updates directly from Fedora.  Check out the [mission statement](/mission) and [documentation](https://universal-blue.org/introduction/) for more information.

## What are some of the unique applications that Bazzite uses?

- [Bazzite Portal, also known as YAFTI](https://github.com/ublue-os/yafti/), acts as both a first-boot utility and general software configuration and installation tool.
- [Just](https://github.com/casey/just) is for executing custom commands based on recipes.  Type `just` in a host terminal to see what commands are available.  See some example commands [here](/guide/just/).
- [Fleek](https://getfleek.dev/) is a [Nix](https://search.nixos.org/packages) package manager wrapper and `$HOME` manager using YAML.
- [OBS-Portable OCI Image](https://github.com/ublue-os/obs-studio-portable) is the universal installation method of the [OBS-Portable](https://github.com/wimpysworld/obs-studio-portable) which aims to be OBS Studio with codecs and several popular plugins preinstalled, and as the name implies it's a portable application too.

## I think I installed the wrong Bazzite image!  Do I have to reinstall?

If you installed the wrong Bazzite image or want to use another image then you can switch to another Bazzite or any other Universal Blue image without losing any of user data by **rebasing**.  Enter the command in a host terminal found on this [page](/images/) for whatever image you're looking for.  After it is finished rebasing then reboot your system.

You can also rebase to a stock Fedora imaged-based desktop image by entering in a host terminal `ostree remote refs fedora` to see a list of available Fedora images that you can rebase to.  Afterwards, enter `rpm-ostree rebase <image>` and wait for it to install the image then reboot.

##  How similar is Bazzite to SteamOS on Steam Deck hardware?

It should nearly be identical to the end user overall.  Bazzite Steam Deck images include the latest Gamescope which means we are always ahead of SteamOS in terms of Game Mode features.  The quick access menu (The **...** button that has scaling and framerate settings) is functional for TDP, framerate caps, etc.  Performance should be on par with SteamOS, and every game SteamOS plays should play well on Bazzite.

Third-party software like Decky Loader, Emudeck, RetroDeck, etc. work and can be installed from the Bazzite Portal, but certain tools like CryoUtilities does not work.  If you want the swap functionality from CryoUtilities, then you can switch to swap and adjust the size in the Bazzite Portal, but it's not recommended.  Desktop Mode still has access to all of the applications in Discover that SteamOS has.  The only missing feature that SteamOS has over Bazzite currently is HDR support, but this should change once Fedora supports it.

## Does the Steam Deck image recieve BIOS updates like SteamOS?

Yes it does.  If a BIOS update is available then it will install when you update Bazzite normally.  We even included a special command to **disable** these BIOS updates **at your own risk:** `just disable-bios-updates`.

## What is Wayland and X11?

In short, Wayland and X11 (also known as Xorg or the X Window System) are windowing systems for desktop Linux.

* Wayland is the default for most of the images and the recommended option for Bazzite.
* X11 is a legacy windowing system. While we recommend to stick with Wayland, there may be scenarios where X11 would have to be used. Nvidia GPUs may have issues with Wayland, so X11 is the default for the Nvidia images.

You can swap between the two in the login screen for desktop images, and enter `just _toggle_wayland` in a host terminal for Steam Deck/HTPC/Handheld PC images.

## Why are there no Nvidia images that include Game Mode and Waydroid?

Nvidia's proprietary drivers currently do not work with any of this.  AMD and Intel have open source drivers on Linux and are usaully the far better option to use.  

Hopefully this changes in the future thanks to the upcoming [NVK](https://www.collabora.com/news-and-blog/news-and-events/introducing-nvk.html) project, then most people would not have to bother with Nvidia's closed source driver philosophy and all of the downsides that come with that. 

## For the AMD/Intel desktop images, why run Steam in an Arch Linux Distrobox container as opposed to Flatpak?

Steam is not built with flatpak in mind. Valve does not contribute to it, and as a result there are many workarounds that the Arch package does not have to worry about it. The Steam Deck uses the Arch package, and to stay consistent with SteamOS so do we.

Running Steam in Distrobox has the advantage of using [LatencyFleX](https://github.com/ishitatsuyuki/LatencyFleX) and other packages added to the container.  It can also utilize the latest GPU driver releases without the end user having to worry about ABI considerations.

A user can install the Flatpak Steam at any time and use both verisons of Steam if they desire.

## How do I disable update notifications for desktop images?

Open the directory `/etc/ublue-update/` and open `ublue-update.toml` with a text editor.

Change:
`dbus_notify = true` to `dbus_notify = false`

Notifications for updates are now suppressed.

##  I'm using the Steam Deck image on my HTPC, but there are games that force specific Steam Deck features I do not want like a specific controller layout.  Help?

Open the game's properties and under "LAUNCH OPTIONS", add: `SteamDeck=0 %command%` to force a game's "Steam Deck" features to be turned off.

![image](https://github.com/ublue-os/website/assets/121328689/9175f6b8-5a70-49fe-b270-fbc55e8510c0)

Currently, an example of a game where this is needed is Warframe.  Without this option, you cannot play Warframe on the Steam Deck images with a keyboard and mouse.

## On Steam Deck, Handheld PC, and HTPC images I am stuck updating at 99%, and the changelog is the same after every update.  What gives?

The update indicator is actually faked due to the limitations of Steam itself depending on SteamOS for that progress bar.  There is a set schedule for that to stop showing the progress indicator after a certain time, but sometimes this fails.  If it's still at 99% and it's been an unrealistic amount of time then do not worry about it.  It most likely applied the updates to your system, flatpaks, and distrobox containers.  If you are still paranoid then go into Desktop Mode, open a host terminal, and enter: `ublue-update`, and if it there's no errors, you're good.  That is exactly the same method as how you would update in Game Mode anyways.

As for the changelog, those are for SteamOS and not Bazzite.  Some of it may apply since we share a lot of the same packages, but regardless, it will always show SteamOS changelogs by Valve and has no relation to the updates for Bazzite.  Check our [newsletters](https://universal-blue.org/blog/category/bazzite/) for major changes and features. If you want to see the patch notes in real time, check the newest [commits](https://github.com/ublue-os/bazzite/commits/main) on Github.

## Steam is not starting, what should I do? (Also, I have 2 GPUs.)

This would be out of scope for our project due to it being an issue currently with Steam itself and not Bazzite, but we had enough support tickets surrounding it that we are including the fix in our FAQ.

Recently, Steam breaks if you have hybrid graphics in your PC.  The solution is simply locating the .desktop file for Steam (non-Flatpak versions are located in: `~/.local/share/applications/`) and opening it with a text editor (Kate, Text Editor, etc.), and adding this to the last line under `[Desktop Entry]`:
```bash
PrefersNonDefaultGPU=false
X-KDE-RunOnDiscreteGpu=true
```
Save the file.  Steam should now launch.

Read more about this issue [here](https://github.com/ValveSoftware/steam-for-linux/issues/9940).

##  I am experiencing a bug or want to request a feature! Help!

In order to troubleshoot the issue properly, you should add a log or terminal output of the issue.  

**Example 1:** For a game running on Steam through Proton, go to the game's properties and type `PROTON_LOG=1 %command%` in the launch options section.  Play the game and the log should appear by the appid in your `Home` directory, and make sure to attach that to the issue you have opened.

**Example 2**: For a Flatpak application that has issues, get the Flatpak package name of all installed applications by entering `flatpak list` (you may need to readjust the terminal window to get the package name to fit beforehand.)  After you got the name, enter `flatpak run <flatpak.package.name>` and a console output will appear.  Copy and paste into a text file, save it, and attach it.

Explain your issue or proposal in our [issue tracker](https://github.com/ublue-os/bazzite/issues) or [Github Discussions Page](https://github.com/orgs/ublue-os/discussions/categories/bazzite).

It's always a good idea to try and manually update your system by entering in a host terminal: `rpm-ostree update` and waiting for it to update, and rebooting to see if the issue still persists.  Updates download automatically in the background, but entering this command updates it earlier than the schedule.

One of the goals of this project is to have the convenience of never worrying about having to reinstall the operating system.  However, all of this is new, and there could be some catastrophic issues that can occur.  When the worst-case scenario appears and the only solution is to reinstall Bazzite then please backup your personal files in your `$HOME` directory as well as any drives connected to your device.  Application data for Flatpaks, which is anything installed from Discover or GNOME Software, are stored in your Home directory under `~/.var/app/`.  Make sure you have hidden files enabled in the file manager to see all of your files.

## I would like to contribute to Bazzite.  Where do I start?

Thank you for being so eager to contribute to the project!  Bazzite has a [suggestions thread](https://github.com/orgs/ublue-os/discussions/246) where you can suggest any feedback to the project.  If you want to develop or provide documentation for Bazzite, then read the contributing [guide](/images/bazzite/CONTRIBUTING).  This guide also links to our roadmap for future plans with the project.  Reporting issues is also very helpful to the project.
