Check out the [upstream installation documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) for more information.

Notably:

- Dual boot configurations are not supported. We recommend using your PC's BIOS/UEFI boot menu for dual boot configuration so that each OS has its own disk. 
- Manual partitioning is not supported.

!!! Info "This ISO is experimental"

    This method of consuming Fedora is new, and will not be integrated into Fedora until at least F39. Though this method is typically more reliable than traditional distributions, take care to [read the user guide](https://docs.fedoraproject.org/en-US/fedora-silverblue/) and manage your expectations accordingly. As with all operating systems, make a point to back up the data you care about! 

## Installation Instructions

!!! Info "There is a known issue with Ventoy"

    Currently we are aware of an issue where booting from the ISO with Ventoy leads to a black screen with a cursor and nothing happening. This is due to an upstream bug with Anaconda and the way Ventoy sets up loop mounts. We are working on a workaround to enable this workflow but in the meantime please do not create a new issue on GitHub. You can react with a thumbs up on this [issue](https://github.com/ublue-os/main/issues/108) so we can track how many people want this feature.

Each Universal Blue image can be installed from the boot menu of the installation ISO. If you're using an existing Fedora Silverblue/Kinoite system check out the [image page](/images) for rebasing information (you don't need to reinstall).

For new systems, follow the instructions below: 

[Download the ISO :fontawesome-solid-heart:](https://github.com/ublue-os/main/releases){ .md-button .md-button--primary }

1. Use the [Fedora Media Writer](https://flathub.org/apps/details/org.fedoraproject.MediaWriter) to write the ISO to a USB stick. Mac and Windows users can [download it here](https://getfedora.org/en/workstation/download/). Or use a tool of your choice.
1. Select the image you want to install from the boot menu. The `main` images will work on systems with Intel and AMD GPUs, and the images tagged with `nvidia` include the proper drivers: 
![installer](https://user-images.githubusercontent.com/1264109/230446211-a0c4b2e8-2d31-44cb-9179-202f4b9fc52d.png)
![installer2](https://user-images.githubusercontent.com/1264109/230446224-ae43322f-9e4d-4a17-8133-a8bf6def3e64.png)

!!! Info "Disk check"

    The installer will do an integrity check after you've made a selection, this is normal but can be skipped by hitting Escape. The disk detection step might also take longer than expected.

1. If you are familiar with Anaconda there are a few changes you might notice:

![image](https://user-images.githubusercontent.com/1264109/228308230-4cd981f7-d524-44c3-80ff-49e1b62e58fd.png)

1. "Kickstart Insufficient" is expected, select that item and select the disk to install to and click Done at the top left of the screen. User creation is also done at this step instead of first boot.
1. Ensure the machine is on the network by configuring that, otherwise you will get an error (see below)!
1. Select each screen with a warning triangle and make the selection you want until the screen looks similar to this:

![image](https://user-images.githubusercontent.com/1264109/228308903-d3289faf-8d53-4999-9296-2facc364d07b.png)

1. Continue on with the installation

!!! Warning 

    The progress bar during installation will start, but will not progress until towards the end of installation. Depending on the image size this might take a long time. This may appear as though the installation is stalled.  

![image](https://user-images.githubusercontent.com/1264109/228309296-993f7058-7bc7-4157-b1da-3fe908889e37.png)

When the installationn is complete it will ask you to reboot, then you're done!

## Other gotchas

- Reminder: this is a netinstaller!
- If the network connection is spotty the installation download of the image might stall or time out, resulting in an error below
    - Retrying the installation might help depending on network conditions
    - Using an ethernet connection is usually more reliable
- The generated USB stick will always pull the latest image, you shouldn't need to generate a new USB stick often 
- We are looking for volunteers to help generate proper "offline" ISOs
- If you're still having problems with the ISO you can always [install Fedora Silverblue](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) and then rebase to one of [our images](/images)

## Secure Boot

If you choose to install an nvidia variant of and have secure boot enabled, the installer will automatically use `mokutil` to import the ublue-os nvidia module signing key as a Machine Owner Key (MOK) in your UEFI secure boot database.

During the post-install reboot, your system will prompt to verify enrollment of the key.

The installer uses a default password for MOK enrollment: **ublue-os**

Warning: If you use secureboot and do not enroll the MOK, you will boot to a blank screen, as nouveau has been disabled since nvidia drivers were installed but unable to load without the MOK.

## Video Overview

This video goes over what it should like like, but note that the video refers to multiple ISOs, there is now just one ISO image that you choose to boot off of. The rest of the installation looks the same as the video.  

![type:video](https://www.youtube.com/embed/SaPxDJtjoB8)

## Reporting Issues

Please [file an issue](https://github.com/ublue-os/main/issues) if you encounter any problems. An error screen usually looks like this:  

![229818630-cb7e4fb5-42a4-4890-8e75-f92d0ea8dd5b](https://user-images.githubusercontent.com/1264109/230695149-b2c30851-ead0-46f5-8c28-e6aed2b4f6de.png)
