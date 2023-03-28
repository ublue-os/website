Check out the [upstream installation documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/installation/) for more information.

Notably:

- Dual boot configurations are not supported
- Manual partition is not suppported.

!!! Info These images are experimental

    This method of consuming Fedora is new, and will not be integrated into Fedora until at least F39. Though this method of consumption is typically more reliable than traditional distributions, take care to [read the user guide](https://docs.fedoraproject.org/en-US/fedora-silverblue/) and manage your expectations accordingly. As with all operating systems, make a point to back up the data you care about! 

It is recommended to use your PCs BIOS/UEFI boot menu for dual boot configurations so that each OS has its own disk. 

## Installation Instructions

Each uBlue image has a corresponding netinstall ISO (~670MB) that will install that custom image onto your PC

1. Download the ISO of your choice
2. Use the [Fedora Media Writer](https://flathub.org/apps/details/org.fedoraproject.MediaWriter) to write the ISO to a USB stick. Mac and Windows users can [download it here](https://getfedora.org/en/workstation/download/). Or use a tool of your choice.
3. If you are familiar with Anaconda there are a few changes you might notice:

![image](https://user-images.githubusercontent.com/1264109/228308230-4cd981f7-d524-44c3-80ff-49e1b62e58fd.png)

"Kickstart Insufficient" is expected, select that item and select the disk to install to and click Done at the top left of the screen. User creation is also done at this step instead of first boot.

Select each screen with a warning triangle and make the selection you want until the screen looks similar to this:

![image](https://user-images.githubusercontent.com/1264109/228308903-d3289faf-8d53-4999-9296-2facc364d07b.png)

!!! Warning 

    The progress bar during installation will start, but will not progress until towards the end of installation. Depending on the image size this might take a long time. This may appear as though the installation is stalled.  

![image](https://user-images.githubusercontent.com/1264109/228309296-993f7058-7bc7-4157-b1da-3fe908889e37.png)

When the installationn is complete it will ask you to reboot, then you're done!
