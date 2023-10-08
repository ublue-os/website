# Waydroid Configuration

Open a host terminal and enter this command to setup Waydroid:

```bash
just init-waydroid
```

## Gapps, ARM translation, and [other goodies](https://github.com/casualsnek/waydroid_script#waydroid-extras-script)

Open a host terminal and enter `just configure-waydroid`

## SELinux in permissive mode (only if you have issues with any of the above!)

SELinux is a kernel module used by Fedora (and thus Bazzite) to increase security on a Linux system. 
There may be an issue with SELinux file re-labeling in OCI images that prevents Waydroid from being used without SELinux being set to permissive first.

To put SELinux in permissive mode, open a host terminal and enter:

```bash
sudoedit /etc/selinux/config
```

Then, change the line that says:

```bash
SELINUX=enforcing
```

to instead be

```bash
SELINUX=permissive
```

Save this file and reboot.

## Hybrid Graphics Fix

If your PC is running multiple GPUs and you experience graphical corruption then execute this [script](https://raw.githubusercontent.com/Quackdoc/waydroid-scripts/main/waydroid-choose-gpu.sh) to fix it.

## Reset Waydroid
!!! note
 This will delete all of your current Waydroid data!

Enter `just reset-waydroid` if you run into any major issues.
