---
date: 2023-09-28
comments: true
authors: 
  - castrojo
categories:
  - bazzite
  - surface
  - asus
  - bluefin
links:
  - Asus Documentation: https://universal-blue.org/images/asus/
  - Framework Documentation: https://universal-blue.org/images/framework/
  - Surface Documentation: https://universal-blue.org/images/surface/
---
# Announcing expanded support for Asus, Framework and Surface Devices

Over the past few weeks contributors [reworked parts of our build system](https://github.com/ublue-os/main/issues/356) to  support more hardware. Reusing cloud patterns allows Universal Blue to offer [pretty awesome Nvidia support](/images/nvidia/) that's baked right into the image. This has always been a special case, we've now successfully productized the pattern into something that we can repeat quickly.

Devices like certain Asus laptops sometimes need special tools, and these laptops are supported by projects like [asus-linux](https://asus-linux.org/). They not only provide tools, they also hook you up with the right kernels that you need. Similarly, the [linux-surface](https://github.com/linux-surface/linux-surface) project provides special kernels for those devices. They provide the tools and repositories needed to get Fedora working great on those devices. But you have to set that up by hand. Ewww. 

![Bazzite on a Surface](https://github.com/ublue-os/website/assets/1264109/f916e5ec-351d-4157-8d8e-6afd4899f08c)


One of the strengths of the cloud-native pattern is our ability to use existing Fedora base images, and then automate the post-installation steps as new composable layers, and then mix and match what we need. Both Asus and Surface devices can also come with Nvidia cards, which means we can use the existing Nvidia images to help us compose Nvidia-enabled images on top of the good stuff we need from asus-linux and linux-surface! These are now ready to test!  

- [ublue-os/nvidia](https://github.com/ublue-os/nvidia) are the same as the main images but include slip-streamed Nvidia drivers
- [ublue-os/asus](https://github.com/ublue-os/asus) - Asus images
- [ublue-os/asus-nvidia](https://github.com/ublue-os/asus-nvidia) - Asus with Nvidia images
- [ublue-os/framework](https://github.com/ublue-os/framework) - Framework images
- [ublue-os/surface](https://github.com/ublue-os/surface) - Surface images
- [ublue-os/surface-nvidia](https://github.com/ublue-os/surface-nvidia) - Surface with Nvidia images

## The Framework Experiment

The [Framework 13 laptop](https://community.frame.work/t/custom-fedora-oci-images-for-framework-laptops/34253?u=jorge_castro) was a unique prototype in this. Initially only available as a custom spin of [Bluefin](/images/bluefin) to gauge interest. We've reworked that repo to line up with the rest, so instead of being Bluefin-specific you can now enjoy a [wider variety of images](https://github.com/orgs/ublue-os/packages?repo_name=framework) for your Framework.

If you're wondering if we plan on supporting the Framework 16 and new AMD Framework 13 then you're in luck, it's just another set of parameters we can add. We're hoping to get feedback from folks who get this hardware so we can enable it! 

![PXL_20230717_145444220](https://github.com/ublue-os/website/assets/1264109/b3acde75-6d04-4208-bf0f-bf0b10f02f01)


## Why do it this way?

Both asus-linux and linux-surface have existed for a long time, what's the benefit of doing it this way? We list these benefits in [Why would I use these?](/#why-would-i-use-these), but these images are a real world example of how the pattern works.

Both of these projects have done the hard work and provided the community with the right bits. All we do is automate that and run it every night and on every merge. If it works, it ends up on your machine, if it doesn't work, your machine still works. It's broken in our GitHub repository and it doesn't get to you. Instead we use the built-in advantage that we get with open source: It's easier to fix things when you do it together. When the nerds figure it out, the builds pass, and THEN you get the image on your machine. GitOps for the win!

The one gotcha is that we still need to do some post-installation steps manually. You might have had to do this as part of installation, where we ask you to do a `just framework-13` or `just nvidia-set-kargs` in order to get the right kernel parameters in place. We expect this limitation to go away someday and hope to declare kernel arguments directly in the Containerfile. 

## Testers Wanted!

The amount of images we're generating is getting larger, so give these a spin and let us know how you get on! 
