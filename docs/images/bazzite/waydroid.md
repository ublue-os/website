# Waydroid Configuration
!!! note

    Nvidia images are not supported.

Open a host terminal and enter this command to setup Waydroid:

```bash
just init-waydroid
```

## Gapps, ARM translation, and [other goodies](https://github.com/casualsnek/waydroid_script#waydroid-extras-script)

Open a host terminal and enter `just configure-waydroid`.

## Google Play Certification (Recommended)

Run Waydroid and open a host terminal window and run:

```bash
sudo waydroid shell
```

Inside the Waydroid shell (It should just say `:/ #` before the text cursor), enter this command:

```bash
ANDROID_RUNTIME_ROOT=/apex/com.android.runtime ANDROID_DATA=/data ANDROID_TZDATA_ROOT=/apex/com.android.tzdata ANDROID_I18N_ROOT=/apex/com.android.i18n sqlite3 /data/data/com.google.android.gsf/databases/gservices.db "select * from main where name = \"android_id\";"
```

When you run this command, your terminal should output `android_id|` and some numbers. Copy the **numbers**, then visit [this website](<https://www.google.com/android/uncertified>).

Paste the number in the box that says "Google Services Framework ID", answer the captcha (If one is present), then hit register. You should see a popup saying "Device Registered" on the bottom left.

You can now type `exit` in your terminal to leave the Waydroid shell.

Stop the Waydroid container.
```bash
waydroid session stop
```

Relaunch Waydroid and you should now have Google Play certification.

## Hybrid Graphics Fix

If your PC is running multiple GPUs and you experience either graphical corruption or Waydroid does not launch, then execute this [script](https://raw.githubusercontent.com/Quackdoc/waydroid-scripts/main/waydroid-choose-gpu.sh) to fix it.  

Easiest way to run this script is to copy all of this text into a text file save it as `waydroid_fix.sh` to your Home directory.  Open a host terminal and entering: 
```bash
sudo ./waydroid_fix.sh
```
Then select your dedicated GPU.

## Reset Waydroid
!!! note
 This will delete all of your current Waydroid data!

Enter `just reset-waydroid` if you run into any major issues.
