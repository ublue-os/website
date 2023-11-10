# Just commands for Bazzite-deck
Make sure to check out our main [documentation](https://universal-blue.org/guide/just/) on Just. Open a host terminal and type `just <command>`.  Each just command is listed below.  Some of these are exclusive to certain Bazzite images.

## ujust enable-gamescope-autologin
Makes bazzite start in gamescope (game mode), with desktop mode being accessible by the power menu.

## ujust enable-desktop-autologin
Makes Bazzite start in desktop mode, with game mode being accessible via the return to game mode shortcut.

!!!note
    Enabling desktop-autologin currently breaks returning to game mode!

## ujust configure-waydroid
Automatically downloads and runs the waydroid_script repo, to download certain packages (Usually used for ARM emulation) on to your Waydroid install.

## ujust get-decky
Downloads and installs "Decky Loader".

## ujust get-emudeck
Downloads the EmuDeck installer.

## ujust get-steamcmd
Downloads and installs steamcmd.

## ujust install-nix
Downloads and installs the nix package manager.

## ujust remove-nix
Uninstalls the nix package manager.

## ujust get-greenlight
Downloads and installs the greenlight client, an app used for streaming from gamepass and Xbox consoles.

## ujust get-boilr
Downloads and installs Boilr.

## ujust fix-tf2-tcmalloc
Fixes a common crash in Team Fortress 2

## ujust enable-vapor-theme
Enables the Vapor theme, which emulates the default look of SteamOS.

!!!note
    This only works on GNOME. To enable Vapor on KDE, use system settings on your desktop.

## ujust enable-vgui2-theme
Enables the VGUI2 theme, which emulates the old Steam Greeen aesthetic.

note!!!
    This only works on GNOME. To enable VGUI2 on KDE, use system settings on your desktop.

## ujust deckswap-on
Enables swap on your system. (Default: Swap off)

## ujust deckswap-off
Disables swap on your system. (Default: Swap off)

## ujust resize-deckswap
Resizes your swap file in Gigabytes. (Default: 1)

!!!note
    You do not need to use this unless deckswap is also enabled, which it is not by default.

## ujust switch-to-ext4
Switches SD card formatting from BTRFS to ext4. This saves less space, however mimicks the default behaviour of SteamOS. (Default: Off)

## ujust zram-on
Enables ZRAM on your system. (Default: ZRAM on)

## ujust zram-off
Disabled ZRAM on your system. (Default: ZRAM on)

## ujust resize-zram
Resizes ZRAM in Megabytes. (Default: 1024)

!!!note
    You do not need to use this unless ZRAM is also enabled, which it is by default.

## ujust hide-grub
Enables the hiding of the GRUB bootloader (Default: GRUB hidden)

## ujust unhide-grub
Disables the hiding of the GRUB bootloader (Default: GRUB hidden)

## ujust enable-deck-bios-firmware-updates
Enables BIOS/Firmware updates for the Steam Deck

## ujust disable-deck-services
Disables all Steam Deck related services such as fan control for non-deck systems.

## ujust disable-bios-updates
Disables BIOS updates on the Steam Deck.

## ujust disable-firmware-updates
Disables BIOS firmware on the Steam Deck.

## ujust _toggle_wayland
Toggles the display server used on your system to/from X11 or Wayland, depending on what you are using when the command is run.

## ujust sign-image
Switches your Bazzite install to the signed image.
