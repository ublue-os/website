# FAQ

## Why is it called Bazzite?

Fedora's image-based variants are usually named after either [minerals](https://fedoraproject.org/kinoite/) or [flowers](https://fedoraproject.org/sericea/).
## How do I install Bazzite onto my device?

Follow this [guide](/images/bazzite/installation/).

## Can I dual/multi-boot?

Windows dual-booting can be made to work, but is **not recommended** since Windows has a habit of destroying your boot loader.  The best method would be running Windows on a different drive than the one containing Bazzite, like an external one.  Other Linux distributions **should not** be dual/multi-booted due to how Bazzite mounts certain things.

## How do I run Windows applications?

* Use Lutris (preinstalled).
* [Bottles](https://flathub.org/apps/com.usebottles.bottles) for general purpose applications or as an alternative to Lutris.
* [Heroic](https://flathub.org/apps/com.heroicgameslauncher.hgl) for Epic, GOG, and Amazon Games Launcher.

## How do I run Android applications?

Follow the [Waydroid guide](/images/bazzite/waydroid/).

## How do updates work?

### **For *bazzite*, *bazzite-nvidia*, *bazzite-gnome*, and *bazzite-gnome-nvidia*:**

System updates happen automatically daily.  They will be downloaded in the background and will apply on shutdown.  No forced reboots or worrying about manually updating your system.

Flatpak applications (installed from *Discover* or *GNOME Software*) update twice a day automatically.

You can however force update to the whole system (base packages, applications, and containers) at any time by opening your host terminal and entering `just update` then reboot your device after it has finished.

### **For *bazzite-deck* and *bazzite-deck-gnome*:**

Similar to SteamOS, updates are handled by Steam.  In Game Mode, go to Settings > System > click "Apply"

Alternatively, you can open a host terminal and enter `just update` then reboot your device after it has finished.

## How do I install additional software?

### Flatpak

Typically it is recommended to use Flatpak for most software.  These can be installed via the software center that is preinstalled like *Discover* or *GNOME Software*.  Take a look at the [selection](https://flathub.org/apps/collection/popular/1).

### AppImage

AppImages can be installed by downloading any file with an `.AppImage` extension.  These are usually found on a project's website, [Appimage Hub](https://www.appimagehub.com/) or if you install [Appimage Pool](https://flathub.org/apps/io.github.prateekmedia.appimagepool). Then giving the AppImage application executable permssions in the file's properties to run.

!!! Note
    AppImages are not supported in other Universal Blue images.

### Distrobox

Distrobox containers can be made with the host terminal following this [documentation](https://github.com/89luca89/distrobox/blob/main/docs/usage/distrobox-create.md). Keep in mind that `bazzite-arch` is a `distrobox` container that uses `pacman` as the package manager and can utilize the [AUR](https://aur.archlinux.org/).

You can use [other distributions](https://github.com/89luca89/distrobox/blob/main/docs/compatibility.md#containers-distros) inside their own containers.

### Nix

If you opted to use Nix packages at the first boot, then you can use the Nix package manager.  More information on that [here](https://zero-to-nix.com/).

### rpm-ostree

Fedora has [documentation](https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/package-management/rpm-ostree/) on rpm-ostree.

## Do I have to reboot after every `system` update or layering a package?

No. They just won't apply until shutdown.  You can attempt to layer package(s) without rebooting with `rpm-ostree install --apply-live <package>` but sometimes this still requires a reboot depending on the package(s) you installed.

## Why use Fedora? SteamOS is based on Arch Linux.

SteamOS is based on Arch Linux, but the base packages and drivers get updates at a much slower pace than using vanilla Arch and updating yourself. Bazzite will follow Fedora's updates which means it will always be ahead of SteamOS in terms of newer software and drivers.

## How does Bazzite differ from other Linux distributions?

Like SteamOS, Bazzite makes use of read-only root files for stability purposes.

Bazzite is built off of desktop versions of Fedora built with [libostree](https://ostreedev.github.io/ostree/) which has advantages such as:

* Atomic upgrades.
* Containerized applications. (**No dependency hell!**)
* Overlay system packages to the host.
* Smoother upgrade process from major Fedora point releases.
* Very little risk of a non-booting or broken system.
* Rollback system updates.

Check out the [Universal Blue homepage](https://universal-blue.org) for more information.

## Is this another fringe distro?

No. Bazzite is not a distribution. This is Fedora Kinoite/Silverblue (depending on the desktop environment you choose) with a recipe on top of it.  

Unlike traditional Linux distributions, much of the maintenance and security updates are done upstream by Fedora and Universal Blue while Bazzite only configures a great gaming experience out of the box. Check the [mission statement](/mission) for more information.

## For the desktop edition, why run Steam in an Arch Linux Distrobox container as opposed to Flatpak?

Steam is not built with flatpak in mind. Valve does not contribute to it, and as a result there are many workarounds that the Arch package does not have to worry about it. The Steam Deck uses the Arch package, and to stay consistent with SteamOS so do we.

Distrobox Steam has the advantage of using [LatencyFleX](https://github.com/ishitatsuyuki/LatencyFleX) can be added to the container.  SIt can utilize the latest and greatest Mesa drivers without ABI considerations too.

Also currently there is a [minor performance impact](https://github.com/flatpak/flatpak/issues/4187) if you run/attempt to run Flatpak games. However you would really only notice this in edge cases anyways.
## Why isn't Night Mode or color saturation working on my Steam Deck?

For some users, Night Mode or color saturation settings only seem to work when in the home screen or when the QAM or Steam menus are present. To fix this, enable Developer Mode in Settings, General. Then, in the newly accessible Developer menu at the bottom of Settings, enable Force Composite.
