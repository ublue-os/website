# Useful Websites
* [ProtonDB](https://www.protondb.com/) - User reports for games running through proton or have a Linux port. 
* [Are We Anti-Cheat Yet?](https://areweanticheatyet.com/) - List of popular games utilizing anti-cheat software and how well they run on Linux.
* [PC Gaming Wiki](https://www.pcgamingwiki.com/wiki/Home) - General information, workarounds, and enhancements with PC games.
* [General Emulation Wiki](https://emulation.gametechwiki.com/index.php/Main_Page) - Wiki dedicated to video game emulation.


# Steam
* Currently Steam only allows whitelisted games to run by default.
* You can change this by going into the Steam settings > Compatibility > Check "Enable Steam Play for all other titles."

![image](https://github.com/ublue-os/website/assets/121328689/88b3c516-5bf8-47ab-b013-11d23c9f7b84)
![image](https://github.com/ublue-os/website/assets/121328689/d7a55d50-e6cb-46d9-8708-c64adf5fcd13)

* Games with a native Linux port will use that by default
* If the game runs better in Proton you can force it to run a specific version by going into the game's properties > Compatibility > Force the use of a specific Steam Play compatibility tool.

![image](https://github.com/ublue-os/website/assets/121328689/cbc4d1b8-db18-49a1-a552-c478cd1868c7)
![image](https://github.com/ublue-os/website/assets/121328689/25493df4-689e-42d0-8fb1-0d7bb080e755)

# Non-Steam Games
* **It is recommended to use Lutris for _most_ non-steam games.**
* However using Heroic for Epic, GOG, and Amazon Games Launcher would be easier for those specific launchers.
* Bottles is also a good alternative if you wish to use that.
* A few games and/or launchers are avalaible in the software center (_Discover, GNOME Software_) like itch.io.

## Lutris

A lot of non-steam games can be easily installed by searching for it and using Lutris scripts.

![image](https://github.com/ublue-os/website/assets/121328689/ff54c7e4-3b1f-4742-9528-a7db93d33ea5)
![image](https://github.com/ublue-os/website/assets/121328689/046c2c98-5d71-4599-9a73-672b753631ea)

However if your game is not listed or has a broken script, you can manually add the executable.  Here is an example of what your game options should look like roughly.

![image](https://github.com/ublue-os/website/assets/121328689/3a2a09cd-2597-49ba-8e3a-c8f152284ba2)
![image](https://github.com/ublue-os/website/assets/121328689/a8822f49-691d-4bb3-a43c-43592ceba003)

## What is a Proton/WINE Prefix?
Simply, it's the glue that holds everything together when you run a game through WINE/Proton.  It also is responsible for containing any of the files the game would drop outside of the installation folder. (i.e. .../steamapps/common/game)

Tons of PC games drop files in Windows folders like "My Documents" or "Appdata\Roaming" and these files are dropped in the prefix.

For games on Steam, they are located in your ~/.steam/root/steamapps/compatdata/ and then the ID number of the game.  Continue to .../pfx/drive_c/ and wherever the game drops the file on Windows.

Non-Steam games can have the prefix folder anywhere you specify, but by default Lutris likes to use ~/.wine as the main folder.  Sometimes it's in ~/Games too.

# Extras

* Recommended to use ProtonUp-Qt to grab the latest [GE-Proton](https://github.com/GloriousEggroll/proton-ge-custom) and [Luxtorpeda](https://github.com/luxtorpeda-dev/luxtorpeda) for Steam.
* May want to install Protontricks for certain games that may need it.
* You can install [AUR](https://aur.archlinux.org/) and pacman packages with bazzite-arch.
