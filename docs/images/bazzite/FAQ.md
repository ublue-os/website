# FAQ

## Why is it called Bazzite?

Fedora's image-based variants are usually named after either [minerals](https://fedoraproject.org/kinoite/) or [flowers](https://fedoraproject.org/sericea/).
## How do I install Bazzite onto my device?

Follow this [guide](/images/bazzite/installation/).

## Can I dual/multi-boot?

Windows dual-booting can be made to work, but is **not recommended** since Windows has a habit of destroying your boot loader.  The best method would be running Windows on a different drive than the one containing Bazzite, like an external one.  Other Linux distributions **should not** be dual/multi-booted due to how Bazzite mounts certain things.  However you can probably do it if the other Linux OS is on a separate drive.

## I am having issues installing Bazzite onto my hardware.

OCI images are very new and the Fedora installer, Anaconda, has some issues with this.  If you have skills in [Lorax](https://weldr.io/lorax/f28-branch/lorax.html) and the [Anaconda installer](https://www.fedoraproject.org/wiki/Anaconda), please help by contributing!  We are at a crossroads here because this is one of the most difficult hurdles that Bazzite and the Universal Blue project face.  We are essentially dependent on upstream to resolve the issues.

**Here are the main installer issues and their workarounds:**

### Why is my installer not working (dracut issue / black screen)

This is currently a known [issue](https://github.com/ublue-os/bazzite/issues/109).  There is a [workaround](https://github.com/ublue-os/bazzite/issues/109#issuecomment-1691090533) that requires either the stock Fedora Silverblue or Fedora Kinoite ISO and rebasing to Bazzite from there after installation.  
!!! warning

    Keep in mind that the Steam Deck will not scale properly with the installer, and the buttons on the bottom of the screen will be cut off.  This will require use of the `TAB` key on your keyboard to navigate the installer blindly.

There is also two other **alternaitve** methods that may work:  
Installing with basic graphics mode in the installer or using this [advanced guide](https://sharing.io/deck.html).

Keep in mind we do not support booting using Ventoy.

### Error occured while installing the payload

Make sure you are connected to the internet if you are using an online ISO.  If you are, and there is still an issue, there might be an issue with your network adapter and Linux.  Recommended to use a wired connection if you can if this occurs.

### Black screen on boot and there are no logs

Remove the `rd.live.check` line from the boot parameters in grub. Press <kbd>E</kbd> on a physical keyboard when you see the boot option.  After removing that line, press <kbd>CTRL</kbd>+<kbd>X</kbd> to save.  It should boot now, and this line skipped the media verification which is the default behavior in the installer.

## I am new to Linux gaming.  Where do I start?

We have a gaming starter guide [here](/images/bazzite/gaming_guide).  If you own a Steam Deck then it should be a similar experience.

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

### rpm-ostree

Fedora has [documentation](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/rpm-ostree/) on rpm-ostree.  The most common command you will use is `rpm-ostree install <package>` to layer Fedora's RPM packages to the image.  After that has finished you will be required to reboot your system to use it.  However, it is highly recommended to only use this command as the last resort especially if the package can be obtained through the above methods.

## How do I run Windows applications?

* Use Lutris (preinstalled).
* [Bottles](https://flathub.org/apps/com.usebottles.bottles) for general purpose applications or as an alternative to Lutris.
* [Heroic](https://flathub.org/apps/com.heroicgameslauncher.hgl) for Epic, GOG, and Amazon Games Launcher.

## How do I run Android applications?

Follow the [Waydroid guide](/images/bazzite/waydroid/).

## How do updates work?

### Desktop images (*bazzite*, *bazzite-nvidia*, *bazzite-gnome*, and *bazzite-gnome-nvidia*, etc.)

System updates happen automatically daily.  They will be downloaded in the background and will apply on shutdown.  No forced reboots or worrying about manually updating your system.

Flatpak applications (installed from *Discover* or *GNOME Software*) update twice a day automatically.

You can however force update to the whole system (base packages, applications, and containers) at any time by opening your host terminal and entering `just update` then reboot your device after it has finished.

### Steam Deck and HTPC images (*bazzite-deck* and *bazzite-deck-gnome*, etc.)

Similar to SteamOS, updates are handled by Steam.  In Game Mode, go to Settings > System > click "Apply"

Alternatively, you can open a host terminal and enter `just update` then reboot your device after it has finished.

## Do I have to reboot after every system update or layering a package?

No. They just won't apply until shutdown.  You can attempt to layer package(s) without rebooting with `rpm-ostree install --apply-live <package>` but sometimes this still requires a reboot depending on the package(s) you installed.

## How do I rollback a system update?

Read Fedora's official [documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/updates-upgrades-rollbacks/#rolling-back) on this.  You can pin your current deployment with `sudo ostree admin pin 0` in a host terminal.  You can also rollback in the GRUB menu.

## Why use Fedora? SteamOS is based on Arch Linux.

SteamOS is based on Arch Linux, but the base packages and drivers get updates at a much slower pace than using vanilla Arch and updating yourself. Bazzite will follow Fedora's updates which means it will always be ahead of SteamOS in terms of newer software and drivers.

## How does Bazzite differ from other Linux distributions?

Like SteamOS, Bazzite makes use of read-only root files for stability purposes.

Bazzite is built off of desktop versions of Fedora built with [libostree](https://ostreedev.github.io/ostree/) which has advantages such as:

* Atomic upgrades.
* Containerized applications which means dependencies issues should rarely happen.
* Overlay system packages to the host.
* Smoother upgrade process from major Fedora point releases.
* Very little risk of an unbootable or broken system.
* Rollback system updates.

Check out the [Universal Blue homepage](https://universal-blue.org) for more information.

## Is this another fringe distro?

No. Bazzite is not a distribution. This is Fedora Kinoite/Silverblue (depending on the desktop environment you choose) with a recipe on top of it.  A hypothetical scenario where everyone involved with Universal Blue could stop maintaining the project and it will still continue to receive updates directly from Fedora.  We are utilizing the [Open Container Initiative](https://opencontainers.org/) to create these images, and most of these images are simply adding packages, services, etc. Bazzite's goal is Fedora Linux, but it provides a great gaming experience out of the box.

Unlike traditional Linux distributions, much of the maintenance and security updates are done upstream by Fedora and Universal Blue while Bazzite only configures a great gaming experience out of the box. Check out the [mission statement](/mission) and [documentation](https://universal-blue.org/introduction/) for more information.

## What are some of the unique applications that Bazzite uses?

- [Bazzite Portal, also known as YAFTI](https://github.com/ublue-os/yafti/), acts as both a first-boot utility and general software configuration and installation tool.
- [Just](https://github.com/casey/just) is for executing custom commands based on recipes.  Type `just` in a host terminal to see what commands are available.  See some example commands [here](/guide/just/).
- [Fleek](https://getfleek.dev/) is a [Nix](https://search.nixos.org/packages) package manager wrapper and `$HOME` manager using YAML.

## How do I switch to a different Bazzite or other Universal Blue image?

You can rebase to a Bazzite or general Universal Blue image by entering the command in a host terminal found on this [page](/images/).  After it is finished, reboot your system.

You can also rebase to a stock Fedora imaged-based desktop image by entering in a host terminal `ostree remote refs fedora` to see a list of available Fedora images that you can rebase to.  Afterwards enter `rpm-ostree rebase <image>` and wait for it to install the image then reboot.

## For the desktop edition, why run Steam in an Arch Linux Distrobox container as opposed to Flatpak?

Steam is not built with flatpak in mind. Valve does not contribute to it, and as a result there are many workarounds that the Arch package does not have to worry about it. The Steam Deck uses the Arch package, and to stay consistent with SteamOS so do we.

Running Steam in Distrobox has the advantage of using [LatencyFleX](https://github.com/ishitatsuyuki/LatencyFleX) and other packages added to the container.  It can also utilize the latest Mesa drivers releases without the end user having to worry about ABI considerations.

There is a [minor performance impact](https://github.com/flatpak/flatpak/issues/4187) if you run/attempt to run Flatpak games. However it is only noticeable with certain edge cases.

If you so desire, you can still install the Flatpak Steam at any time.

## Does the Steam Deck image recieve BIOS updates like SteamOS?

Yes it does.  If a BIOS update is available then it will install when you update Bazzite normally.  We even included a special command to **disable** these BIOS updates **at your own risk:** `just disable-bios-updates`.

## How do I disable update notifications for desktop images?

Open the directory `/etc/ublue-update/` and open `ublue-update.toml` with a text editor.

Change:
`dbus_notify = true` to `dbus_notify = false`

Notifications for updates are now suppressed.

##  I'm using the Steam Deck image on my HTPC, but there are games force specific Steam Deck features I do not want like a specific controller layout.  Help?

Open the game's properties and under "LAUNCH OPTIONS", add: `SteamDeck=0 %command%` to force a game's "Steam Deck" features to be turned off.

![image](https://github.com/ublue-os/website/assets/121328689/9175f6b8-5a70-49fe-b270-fbc55e8510c0)

Currently, an example of a game where this is needed is Warframe.  Without this option, you cannot play Warframe on the Steam Deck images with a keyboard and mouse.

##  I am experiencing a bug or want to request a feature!  Help!

In order to troubleshoot the issue properly, you should add a log or terminal output of the issue.  

**Example 1:** For a game running on Steam through Proton, go to the game's properties and type `PROTON_LOG=1 %command%` in the launch options section.  Play the game and the log should appear by the appid in your `Home` directory, and make sure to attach that to the issue you have opened.

**Example 2**: For a Flatpak application that has issues, get the Flatpak package name of all installed applications by entering `flatpak list` (you may need to readjust the terminal window to get the package name to fit beforehand.)  After you got the name, enter `flatpak run <flatpak.package.name>` and a console output will appear.  Copy and paste into a text file, save it, and attach it.

Explain your issue or proposal in our [issue tracker](https://github.com/ublue-os/bazzite/issues) or [Github Discussions Page](https://github.com/ublue-os/bazzite/discussions).

It's always a good idea to try and manually update your system by entering in a host terminal: `rpm-ostree update` and waiting for it to update, and rebooting to see if the issue still persists.  Updates download automatically in the background, but entering this command updates it earlier than the schedule.

One of the goals of this project is to have the convenience of never worrying about having to reinstall the operating system.  However, all of this is new and there could be some catastrophic issues that can occur.  When the worst case scenario appears and the only solution is to reinstall Bazzite then please backup your personal files in your `$HOME` directory as well as any drives connected to your device.  Application data for Flatpaks, which is anything installed from Discover or GNOME Software, are stored in your Home directory under `~/.var/app/`.  Make sure you have hidden files enabled in the file manager to see all of your files.

## I would like to contribute to Bazzite, where do I start?

Thank you for being so eager to contribute to the project!  We have documentation for contributing [here](/images/bazzite/CONTRIBUTING).  This documentation also links to our roadmap for future plans with the project.
