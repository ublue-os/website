---
date: 2023-09-18
comments: true
authors: 
  - nicknamenamenick
categories:
  - bazzite
links:
  - Bazzite Commits: https://github.com/ublue-os/bazzite/commits/main
  - Bazzite 1.0: https://universal-blue.org/blog/2023/08/20/bazzite-10/
---
# Bazzite Buzz No. 3

![](https://hackmd.io/_uploads/BJm93mSka.png)
<p style="text-align: center;font-weight: bold">Type "just" in a host terminal to see a list of custom convenience commands.</p>
<hr>

Welcome to Bazzite Buzz #3! Bazzite is a custom image of Fedora 38 designed to bring the best in Linux gaming to your PC and handheld devices. This newsletter highlights all the work we are working on over the past few weeks. If you are new to a Universal Blue project here's some back filler: These images follow the [continuous delivery](https://continuousdelivery.com/) methodology of development. That means we're constantly adding new things, so let's get started! 

**IMPORTANT:** Nvidia GPU users should recreate the `bazzite-arch` Distrobox container.  Open a host terminal and enter: `just install-bazzite-arch` to do this.  The issue stemmed from missing 32-bit libraries that require the user to remake the container. As a result of this, it unfortunately means this fix requires manual intervention.
<hr>

New hardware support and a ton of general fixes have been the main focus over the last couple of weeks for Bazzite.  Some notable features added were the inclusion of a new system resource monitor application and adding proper support for Microsoft Surface devices.  We also were committed to fixing as many issues reported as we possibly can, and tidying up the project as usual.

![](https://hackmd.io/_uploads/r1WzxTeJa.png)
<p style="text-align: center;font-weight: bold">A modern task manager.</p>

As time goes on, we plan to release an image dedicated to the Asus ROG Ally.  This device needs a specific kernel and some other tweaks to have Bazzite function correctly on it.  Discussion on this can be found [here](https://github.com/ublue-os/bazzite/pull/162), and for progress on general handheld controls take a look [here](https://github.com/ublue-os/bazzite/pull/201).

[Hippie Hacker](https://github.com/hh) has created this [guide](https://sharing.io/deck.html) to get [iimatey](https://github.com/ii/matey) working on a Steam Deck installation of Bazzite for a command line approach to  installing it. This may solve issues with the current GUI installer or for those who prefer this command line interface method for installation.

Finally, most of the new features from the SteamOS 3.5 preview are already available in the Bazzite Steam Deck images right now.  This includes gamescope's new scaling and color options.  We also are already using newer base packages than SteamOS 3.5.

![](https://hackmd.io/_uploads/r1yqzaeJT.png)
<p style="text-align: center; font-weight: bold">New Gamescope improvements on the Steam Deck images.</p>


# Features
- Microsoft Surface devices are now officially supported.
- Broadcom's WL driver can be installed since it is needed by some hardware.  Disabled by default.  Enter `just use-broadcom-wl` to use it.
- Added [Mission Center](https://gitlab.com/mission-center-devs/mission-center) as a preinstalled application.
- Added [Discover Overlay](https://github.com/trigg/Discover) as a preinstalled application.
- Use Valve's defaults in Mesa.
- Mesa updated to 23.1.7
- [OpenRazer](https://github.com/openrazer/openrazer) is now an option in Bazzite Portal.
- Default fonts in the GNOME images match the defaults of SteamOS KDE.
- Added the Ryzen SMU driver to load automatically on Steam Deck builds.
- Added Steam soundfont when selecting a Valve-inspired theme for GNOME images. 
- The GNOME Steam Deck image now has a template for [vkBasalt](https://github.com/DadSchoorse/vkBasalt) to give an example config available from the right click menu.
- Gear Lever can now upgrade Greenlight when an update is available.
- Added disk display information to neofetch.
- Enabled Steam CEF port forwarding by default.
- Steam Deck images now disable PEERNTP, so Network Time Security is always used.
- Flatpak management is now improved through our `flatpak-manager` utility.
- Users can perform system updates as root and allow updates per active user.
- Increased `vm.max_map_count` for S&box and Counter-Strike 2 to function properly w/ Proton.
- Added Nix garbage collection to `just clean-system`
- Added a Just command for enabling theme integration with Flatpak applications.
- Added a Just command to install OBS Studio Portable.
- Added a Just command to disable uBlue gamepad drivers if desired. (Thanks [lorduskordus!](https://github.com/lorduskordus))
- Added a Just command to disable sdgyrodsu.

# Fixes
- Older AMD GPUs will now be detected properly.  (Thanks [Action Retro!](https://www.youtube.com/@ActionRetro))
- Hybrid GPUs using Nvidia + AMD/Intel should be working better now.
- Hardware setup should only retrieve GPU hardware information once. 
- Fixed the GNOME Steam Deck image power profile to have [sensible defaults](https://github.com/ublue-os/bazzite/commit/23347190c7d43f32714d41cd8d10fe150215d1bb).
- Deck services should now be disabled on generic devices on the Steam Deck images.
- Added workaround from ChimeraOS for Gamescope crashing if Steam hasn't been launched prior to switching to Game Mode.
- Oversteer should now work properly once installed from Bazzite Portal or through Just.
- Fixed Boilr installer not working in some scenarios.
- Flatpak lists are now in `/usr` so changes won't be removed.
- The desktop auto-login service has been removed from desktop images, and enhanced on Steam Deck images to check that Steam has been updated prior to starting gamescope session.
- The Team Fortress 2 tcmalloc fix now works when Team Fortress 2 is installed on a microSD.
- Hide GRUB Menu option from Bazzite Portal has been removed from the desktop images since the focus has shifted to the Steam Deck images for home theater PC setups.
- `pulseaudio-utils` has been added since some third-party applications depend on this.
- Fixed missing icon for Lutris.
- Fixed the `xdg-desktop-portals` bug that affected the file picker. 
- Numerous fixes to fish shell.
- Numerous fixes to Bazzite Portal.

Full changelog [here](https://github.com/ublue-os/bazzite/pull/273#issue-1886248136). 
