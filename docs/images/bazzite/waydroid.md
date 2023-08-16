# How to install Waydroid on Bazzite (Steam Deck and Desktop edition)

**NOTE: FOR THE STEAM DECK I HIGHLY RECOMMEND USING AN EXTERNAL DESK SETUP TO GET THIS WORKING, AT MINIMUM A KEYBOARD AND MOUSE IS RECOMMENDED.**

**This guide also has a lot of copy pasting to terminal. To copy from terminal, you use ctrl+shift+c, to paste you use ctrl+shift+v**

## 1. Disabling SELinux and enabling the Waydroid container
SELinux is a kernel module used by Fedora (and thus Bazzite) to increase security on a Linux system. 
Currently there is an issue with SELinux file re-labeling in OCI images that prevents Waydroid from being used without SELinux being disabled first.

To disable SELinux, run:

```
sudo nano /etc/selinux/config
```
Then, change the line that says:

```
SELINUX=enforcing
```
to instead be

```
SELINUX=disabled
```

Then press ctrl+s, then ctrl+x to save and quit.

After this reboot.

Once rebooted, run this command:

```
sudo systemctl enable --now waydroid-container
```

after running that the waydroid container will start and is set to run on any subsequent startup.

## 2. Initializing Waydroid
Initializing Waydroid just means installing Android. To do so, run this command:

```
sudo waydroid init -c https://ota.waydro.id/system -v https://ota.waydro.id/vendor -s GAPPS -f
```

This installs Android along with the Google Play Store.

## 3. Starting Waydroid
You can now test waydroid for the first time! Open Waydroid from your launcher (Start menu). Be ready to move it out of the way or minimize it, because it's going to need to be open for the next few steps

## 4. Google Play Certification
With waydroid open, open a terminal window and run

```
sudo waydroid shell
```

Once you've entered the waydroid shell (It should just say `:/ #` before your text cursor), enter the command:

```
ANDROID_RUNTIME_ROOT=/apex/com.android.runtime ANDROID_DATA=/data ANDROID_TZDATA_ROOT=/apex/com.android.tzdata ANDROID_I18N_ROOT=/apex/com.android.i18n sqlite3 /data/data/com.google.android.gsf/databases/gservices.db "select * from main where name = \"android_id\";"
```

When you run this command, your terminal should output `android_id|` and some numbers. Copy the numbers, then visit [this website](<https://www.google.com/android/uncertified>).

Paste the number in the box that says "Google Services Framework ID", answer the captcha (If one is present), then hit register. You should see a popup saying "Device Registered" in the bottom left.

You can now type `exit` to leave the Waydroid shell.

## 5. Changing the resolution on Waydroid
**Note:** Changing DPI will be done on a later step. This is more relevant on the Steam Deck, just hold tight.

This is pretty easy! Just open up your terminal and enter the following commands. Just change the number at the end to fit whatever display resolution you are using, just as an example I'll show you the commands for 1280x800:

```
waydroid prop set persist.waydroid.width 1280
```

```
waydroid prop set persist.waydroid.height 800

```
We can now exit waydroid by running 

```
waydroid session stop
```
Congrats! If you're running on Bazzite Desktop you can stop here, unless you want ARM emulation in which case skip to **Step 7** for those instructions. The following commands up until step 7 are purely for the Steam Deck.

## 6. Configuring Weston
Weston is a Wayland compositor, which we'll use to get Waydroid working properly in game mode.

First, in your terminal enter:

```
nano ~/.local/this-is-executable.sh

```
and then paste the following:

```
#!/bin/bash

sleep 3
waydroid session stop
WAYLAND_DISPLAY=wayland-1 waydroid show-full-ui
```

Then press ctrl+s and ctrl+x to save and exit.

Next, run this in your terminal:

```
sudo nano ~/.config/weston-waydroid.ini
```
Then paste:

```
[autolaunch]
path=/home/USERNAME/.local/this-is-executable.sh

[output]
name=X1
mode=1920x1080

[output]
name=WL1
mode=1920x1080

[shell]
background-color=0xFF000000
panel-position=none
locking=false
```

Before saving, change USERNAME to your username, and both lines that say mode=1920x1080 to be your desired resolution instead (e.g. mode=1280x800)

Then press ctrl+s and ctrl+x to save and exit.

Finally, run this in your terminal:

```
sudo nano ~/.local/share/applications/weston-waydroid.desktop
```
Then paste the following:

```
[Desktop Entry]
Version=0.1
Type=Application
Name=Weston
Comment=Launch Waydroid nested in Weston
Icon=applications-other
Exec=weston -c /home/USERNAME/.config/weston-waydroid.ini
Actions=
Categories=Utility;
```

Before saving, change USERNAME to your username.

Then press ctrl+s and ctrl+x to save and exit.

Then, run:

```
sudo chmod +x ~/.local/share/applications/weston-waydroid.desktop
```

and

```
sudo chmod +x ~/.local/this-is-executable.sh
```

Congrats! You can now add the weston app to steam (Press add a non-steam app, and it should be in the initial list)! Make sure to change the resolution for weston in game mode to match your display's resolution. It **should** do this by default however I've had issues with it doing so.

## 7. Adding ARM emulation and WideVine
You should now have successfully installed Waydroid, but you may still want to run ARM apps.

To do so, run the following command:

```
git clone https://github.com/casualsnek/waydroid_script && cd waydroid_script && python -m venv venv && source venv/bin/activate && sudo pip install -r requirements.txt && sudo python main.py
```

Now, press enter to select Android 11, press enter to select Install, then press the up and down arrow keys and the space bar to select the following: 
If you're on AMD, select libndk for ARM emulation
If you're on Intel, select libhoudini for ARM emulation
widevine (This allows for rudementary playback for DRM protected streaming services)

Once those are selected, press enter to begin the install. While installing, make sure not to open Waydroid.

Once they're installed, you're done! You can now use ARM apps! Just bare in mind this is emulation, so you're not guaranteed great performance. If you've got a fairly modern CPU it should be good though.

## 8. Waydroid config file (PPI, Fixing GPU stuff etc.)
First, when editing the Waydroid config file you do **not** want Waydroid to be running. So first run:

```
waydroid session stop
```

To edit the waydroid config file run:

```
sudo nano /var/lib/waydroid/waydroid_base.prop
```
To adjust PPI, add this line on the end:

```
ro.sf.lcd_density=100
```

for the Steam Deck, change the number to 215. If you want to calculate your own PPI (I'd recommend this more for other handhelds for correct scaling, it doesn't really matter on Desktops as much) use [this website](<https://www.calculatorsoup.com/calculators/technology/ppi-calculator.php>), then plug that number in. 

If on AMD or Intel GPU's (including the steam deck), change the line that says:

```
ro.hardware.gralloc=gbm
```
to instead be:

```
ro.hardware.gralloc=minigbm_gbm_mesa
```

That's it, you're done!
