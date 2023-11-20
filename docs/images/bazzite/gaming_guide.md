# Linux Gaming Guide

<hr>

<p style="text-align: center; font-weight: 600">ATTENTION:</p>

We are migrating [documentation](https://universal-blue.discourse.group/docs?category=5) to Discourse.  The [Gaming Guide](https://universal-blue.discourse.group/docs?topic=31) is updated over there and this page will soon be removed.

<hr>

## Useful Websites

* [ProtonDB](https://www.protondb.com/) - User reports for games running through proton or have a Linux port. 
* [Are We Anti-Cheat Yet?](https://areweanticheatyet.com/) - List of popular games utilizing anti-cheat software and how well they run on Linux.
* [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Home) - General information, workarounds, and enhancements with PC games.
* [General Emulation Wiki](https://emulation.gametechwiki.com/index.php/Main_Page) - Wiki dedicated to video game emulation.

# Filesystem
!!! Notice
    **If you are coming from Windows, backup your current drives because Linux does not play well with NTFS, and any current secondary drives would have to be reformatted to ext4 or btrfs.**

Most of the time, the average user will spend time in their `Home` directory, since that is where most of the user files will be located.  `Home` will include anything from personal files (like Documents, Videos, Pictures, Music, etc.) to application data.  Applications installed from the software center will have their userdata specifically located in `~/.var/app/`

Where is this `~/.var` mentioned above, and where is the Steam folder?  These are hidden directories. You can show hidden files by clicking the hamburger menu (3 horizontal lines near the top right of your file manager) and select "Show Hidden Files" to see every directory and file that is hidden by default.  They all start with a "." before it.

If you have multiple drives, like a drive where you plan to play your video games from, you can mount it and set it up with KDE Partition Manager (KDE images) or GNOME Disks (GNOME images).

## Steam

Steam can run Windows games on Linux.  It utilizes a wide range of projects like WINE, DXVK, VKD3D, and a bunch of patches all packed into a piece of software built-in to Steam called Proton.

### Enabling Proton for all Steam Games

!!! Info
    **Skip this section if you're using a Steam Deck / Handheld PC / HTPC image**

* Currently Steam only allows whitelisted games to run by default.
* You can change this by going into the Steam settings > Compatibility > Check "Enable Steam Play for all other titles."

![image](https://github.com/ublue-os/website/assets/121328689/88b3c516-5bf8-47ab-b013-11d23c9f7b84)
![image](https://github.com/ublue-os/website/assets/121328689/d7a55d50-e6cb-46d9-8708-c64adf5fcd13)

### Forcing a specific Proton / Steam Play Tool Version

!!! Note
    If you're using a device with an older GPU that does not support Vulkan 1.3 or later, you need to use older Proton and Wine builds like Proton/WINE 6 or earlier.  Even older devices may need to resort to WINED3D for OpenGL translation, which performs much worse.  Check which Vulkan version your GPU uses, enter `vulkaninfo | grep 'Instance Version'` in a terminal.

* Games with a native Linux port will be used first by default on desktop images.
* Valve selects the default runner on Steam Deck, HTPC, and Handheld PC images.
* If the game runs better with a specific Proton then you can force it to run that specific version by going into the game's properties > Compatibility > Force the use of a specific Steam Play compatibility tool.

![image](https://github.com/ublue-os/website/assets/121328689/cbc4d1b8-db18-49a1-a552-c478cd1868c7)
![image](https://github.com/ublue-os/website/assets/121328689/25493df4-689e-42d0-8fb1-0d7bb080e755)

## Non-Steam Games

* **It is recommended to use Lutris for _most_ non-steam games.**
* However using [Heroic](https://heroicgameslauncher.com) for Epic, GOG, and Amazon Games Launcher would be easier for those specific launchers.
* [Bottles](https://usebottles.com/) is also a good alternative if you wish to use that.
* Other games and launchers are available in the software center (_Discover, GNOME Software_) like Xonotic and itch.io.

### Lutris

[A large portion of non-steam games](https://lutris.net/games) can be easily installed by searching for it and using Lutris scripts.

![image](https://github.com/ublue-os/website/assets/121328689/ff54c7e4-3b1f-4742-9528-a7db93d33ea5)
![image](https://github.com/ublue-os/website/assets/121328689/046c2c98-5d71-4599-9a73-672b753631ea)

However if your game is not listed or has a broken script, you can manually add the executable. Here is an example of what your game options should roughly look like.

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

## Modding Quickstart

- Steam Workshop is the easiest way to obtain mods, but is not supported for every title and requires you to own the game on Steam.  
- You can still add or replace files and directories, but there may be some extra steps on the Linux desktop.
- Some mods require a "WINE DLL OVERRIDE" environment variable like `WINEDLLOVERRIDES="dinput8=n,b" %command%` or something similar.
- You can also play around with [Steam Tinker Launch](https://github.com/sonic2kk/steamtinkerlaunch) which can be installed via ProtonUp-Qt (for KDE images) or ProtonPlus (for GNOME images.)

## Extras

* It is recommended to use ProtonUp-Qt or ProtonPlus (included on Bazzite) to update the latest [GE-Proton](https://github.com/GloriousEggroll/proton-ge-custom) and [Luxtorpeda](https://github.com/luxtorpeda-dev/luxtorpeda) for Steam, and it also includes other useful SteamPlay tools.
* Some games require Protontricks (included) or Winetricks (for non-Steam games, included with Lutris) to function properly.
* You can overlay [RPM](https://packages.fedoraproject.org/) packages to the host by using `rpm-ostree install <package>` in your host terminal **at your own risk.**


<hr>

[<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 496 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg>](https://github.com/ublue-os/bazzite)  [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M524.531,69.836a1.5,1.5,0,0,0-.764-.7A485.065,485.065,0,0,0,404.081,32.03a1.816,1.816,0,0,0-1.923.91,337.461,337.461,0,0,0-14.9,30.6,447.848,447.848,0,0,0-134.426,0,309.541,309.541,0,0,0-15.135-30.6,1.89,1.89,0,0,0-1.924-.91A483.689,483.689,0,0,0,116.085,69.137a1.712,1.712,0,0,0-.788.676C39.068,183.651,18.186,294.69,28.43,404.354a2.016,2.016,0,0,0,.765,1.375A487.666,487.666,0,0,0,176.02,479.918a1.9,1.9,0,0,0,2.063-.676A348.2,348.2,0,0,0,208.12,430.4a1.86,1.86,0,0,0-1.019-2.588,321.173,321.173,0,0,1-45.868-21.853,1.885,1.885,0,0,1-.185-3.126c3.082-2.309,6.166-4.711,9.109-7.137a1.819,1.819,0,0,1,1.9-.256c96.229,43.917,200.41,43.917,295.5,0a1.812,1.812,0,0,1,1.924.233c2.944,2.426,6.027,4.851,9.132,7.16a1.884,1.884,0,0,1-.162,3.126,301.407,301.407,0,0,1-45.89,21.83,1.875,1.875,0,0,0-1,2.611,391.055,391.055,0,0,0,30.014,48.815,1.864,1.864,0,0,0,2.063.7A486.048,486.048,0,0,0,610.7,405.729a1.882,1.882,0,0,0,.765-1.352C623.729,277.594,590.933,167.465,524.531,69.836ZM222.491,337.58c-28.972,0-52.844-26.587-52.844-59.239S193.056,219.1,222.491,219.1c29.665,0,53.306,26.82,52.843,59.239C275.334,310.993,251.924,337.58,222.491,337.58Zm195.38,0c-28.971,0-52.843-26.587-52.843-59.239S388.437,219.1,417.871,219.1c29.667,0,53.307,26.82,52.844,59.239C470.715,310.993,447.538,337.58,417.871,337.58Z"/></svg>](https://discord.bazzite.gg/) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 640 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M208 352c114.9 0 208-78.8 208-176S322.9 0 208 0S0 78.8 0 176c0 38.6 14.7 74.3 39.6 103.4c-3.5 9.4-8.7 17.7-14.2 24.7c-4.8 6.2-9.7 11-13.3 14.3c-1.8 1.6-3.3 2.9-4.3 3.7c-.5 .4-.9 .7-1.1 .8l-.2 .2 0 0 0 0C1 327.2-1.4 334.4 .8 340.9S9.1 352 16 352c21.8 0 43.8-5.6 62.1-12.5c9.2-3.5 17.8-7.4 25.3-11.4C134.1 343.3 169.8 352 208 352zM448 176c0 112.3-99.1 196.9-216.5 207C255.8 457.4 336.4 512 432 512c38.2 0 73.9-8.7 104.7-23.9c7.5 4 16 7.9 25.2 11.4c18.3 6.9 40.3 12.5 62.1 12.5c6.9 0 13.1-4.5 15.2-11.1c2.1-6.6-.2-13.8-5.8-17.9l0 0 0 0-.2-.2c-.2-.2-.6-.4-1.1-.8c-1-.8-2.5-2-4.3-3.7c-3.6-3.3-8.5-8.1-13.3-14.3c-5.5-7-10.7-15.4-14.2-24.7c24.9-29 39.6-64.7 39.6-103.4c0-92.8-84.9-168.9-192.6-175.5c.4 5.1 .6 10.3 .6 15.5z"/></svg>](https://github.com/orgs/ublue-os/discussions/categories/bazzite) [<svg xmlns="http://www.w3.org/2000/svg" height="2em" viewBox="0 0 512 512"><!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path d="M256 512A256 256 0 1 0 256 0a256 256 0 1 0 0 512zM169.8 165.3c7.9-22.3 29.1-37.3 52.8-37.3h58.3c34.9 0 63.1 28.3 63.1 63.1c0 22.6-12.1 43.5-31.7 54.8L280 264.4c-.2 13-10.9 23.6-24 23.6c-13.3 0-24-10.7-24-24V250.5c0-8.6 4.6-16.5 12.1-20.8l44.3-25.4c4.7-2.7 7.6-7.7 7.6-13.1c0-8.4-6.8-15.1-15.1-15.1H222.6c-3.4 0-6.4 2.1-7.5 5.3l-.4 1.2c-4.4 12.5-18.2 19-30.6 14.6s-19-18.2-14.6-30.6l.4-1.2zM224 352a32 32 0 1 1 64 0 32 32 0 1 1 -64 0z"/></svg>](https://universal-blue.org/images/bazzite/FAQ/)
