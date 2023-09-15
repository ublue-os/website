# Linux Gaming Guide

## Useful Websites

* [ProtonDB](https://www.protondb.com/) - User reports for games running through proton or have a Linux port. 
* [Are We Anti-Cheat Yet?](https://areweanticheatyet.com/) - List of popular games utilizing anti-cheat software and how well they run on Linux.
* [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Home) - General information, workarounds, and enhancements with PC games.
* [General Emulation Wiki](https://emulation.gametechwiki.com/index.php/Main_Page) - Wiki dedicated to video game emulation.

# Filesystem
!!! Notice
    **If you are coming from Windows, backup your current drives because Linux does not play well with NTFS, and any current secondary drives would have to be reformatted to ext4 or btrfs.**

Most of time the average user will be under `Home` since that is where most of the user files will be located.  `Home` will include anything from personal files (like Documents, Videos, Pictures, Music, etc.) to application data.  Applications installed from the software center will be located in `~/.var/app/`

Where is this `.var` mentioned above, and where is the Steam folder?  They are hidden directories. You can show hidden files by clicking the hamburger menu (3 horizontal lines near the top right of your file manager) and select "Show Hidden Files" to see every directory and file that is hidden by default.  They all start with a "." before it.

![image](https://github.com/nicknamenamenick/website/assets/121328689/f427114b-9c97-445d-8498-8e0e919fab2d)
![image](https://github.com/nicknamenamenick/website/assets/121328689/ec367ef3-3893-421c-a4fc-c892f368933d)
Hidden files and Flatpak application data on _bazzite-gnome_.

## Steam

Steam can run Windows games on Linux.  It utilizes a wide range of projects like WINE, DXVK, VKD3D, and a bunch of patches all packed into a piece of software built-in to Steam called Proton.

### Enabling Proton for all Steam Games

!!! Info
    **Skip this section if you're using bazzite-deck or bazzite-deck-gnome**

* Currently Steam only allows whitelisted games to run by default.
* You can change this by going into the Steam settings > Compatibility > Check "Enable Steam Play for all other titles."

![image](https://github.com/ublue-os/website/assets/121328689/88b3c516-5bf8-47ab-b013-11d23c9f7b84)
![image](https://github.com/ublue-os/website/assets/121328689/d7a55d50-e6cb-46d9-8708-c64adf5fcd13)

### Forcing a specific Proton / Steam Play Tool Version

!!! Note
    If you're using a device with an older GPU that does not support Vulkan 1.3 or later, you need to use older Proton and Wine builds like Proton/WINE 6 or earlier.  Even older devices may need to resort to WINED3D for OpenGL translation, which performs much worse.  Check which Vulkan version your GPU uses, enter `vulkaninfo | grep 'Instance Version'` in a terminal.

* Games with a native Linux port will use that by default
* If the game runs better in Proton you can force it to run a specific version by going into the game's properties > Compatibility > Force the use of a specific Steam Play compatibility tool.

![image](https://github.com/ublue-os/website/assets/121328689/cbc4d1b8-db18-49a1-a552-c478cd1868c7)
![image](https://github.com/ublue-os/website/assets/121328689/25493df4-689e-42d0-8fb1-0d7bb080e755)

## Non-Steam Games

* **It is recommended to use Lutris for _most_ non-steam games.**
* However using [Heroic](https://heroicgameslauncher.com) for Epic, GOG, and Amazon Games Launcher would be easier for those specific launchers.
* [Bottles](https://usebottles.com/) is also a good alternative if you wish to use that.
* Other games and launchers are available in the software center (_Discover, GNOME Software_) like Xonotic and itch.io.

### Lutris

[A large portion of non-steam games](ttps://lutris.net/games) can be easily installed by searching for it and using Lutris scripts.

![image](https://github.com/ublue-os/website/assets/121328689/ff54c7e4-3b1f-4742-9528-a7db93d33ea5)
![image](https://github.com/ublue-os/website/assets/121328689/046c2c98-5d71-4599-9a73-672b753631ea)

However if your game is not listed or has a broken script, you can manually add the executable. Here is an example of what your game options should look like, roughly.

![image](https://github.com/ublue-os/website/assets/121328689/3a2a09cd-2597-49ba-8e3a-c8f152284ba2)

![image](https://github.com/ublue-os/website/assets/121328689/a8822f49-691d-4bb3-a43c-43592ceba003)

## What is a Proton/WINE Prefix?

It's the glue that holds everything together when you run a game through WINE/Proton. It also is responsible for containing any of the files the game would drop outside of the installation folder.

*This installation folder for Steam games is usually in*
`.../steamapps/common/<game>`

Many PC games drop files in Windows folders, like My Documents or somewhere in a folder called Appdata, and these files are dropped in the prefix.

This prefix folder may be useful for modding your games, backing up your saves, or where game config files may be.

For games on Steam, they are located in your `~/.steam/root/steamapps/compatdata/` folder, and then the ID number of the game. Continue to `.../pfx/drive_c/` and wherever the game drops the file on Windows.

Non-Steam games can have the prefix folder anywhere you specify, but by default Lutris uses `~/.wine` as the main folder.  Sometimes it's also in `~/Games`.

## Extras

* It is recommended to use ProtonUp-Qt (included) to update the latest [GE-Proton](https://github.com/GloriousEggroll/proton-ge-custom) and [Luxtorpeda](https://github.com/luxtorpeda-dev/luxtorpeda) for Steam.
* You may want to install Protontricks for certain games that may need it.
* You can install [pacman](https://archlinux.org/packages/) and [AUR](https://aur.archlinux.org/) packages inside of the `bazzite-arch` container.
* You can overlay [RPM](https://packages.fedoraproject.org/) packages to the host by using `rpm-ostree install <package>` in your host terminal **at your own risk.**
