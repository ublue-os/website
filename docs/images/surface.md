# Microsoft Surface Images

From the [linux-surface project](https://github.com/linux-surface/linux-surface)

> These days, Linux supports a lot of devices out-of-the-box. As a matter of fact, this includes a good portion of the Microsoft Surface devices—for most parts at least. So why would you need a special kernel for Surface devices? In short, for the parts that are not supported upstream yet.

- [ublue-os/surface](https://github.com/ublue-os/surface) - repository for generating these images

## Changes

Like all Universal Blue images, hardware acceleration and codecs are [included out of the box](/guide/codecs) and the system strives for a zero-maintenance based approach.

- Replaces the stock Fedora kernel with the [Surface kernel](https://github.com/linux-surface/linux-surface/tree/master/pkg/fedora)
- Adds the [correct kernel modules](https://github.com/ublue-os/surface/blob/main/system_files/shared/usr/etc/modules-load.d/ublue-surface.conf) 

## How to Help

Open Source succeeds best when contributors come together to solve a problem. These are areas where contributions would be appreciated:

- Benchmarking tools. It would be nice to be able to run a continuous benchmark that exercises the laptop and can run unattended so that we can automate power testing.

We want to allow Linux users to share this knowledge and expertise with each other to fulfill the true potential of Surface devices. We'll [use science](https://www.youtube.com/watch?v=BABM3EUo990) and the wonders of modern automation to accomplish this!

## Instructions

### Fresh installs


### Rebasing from another image

If you're rebasing from another image follow these instructions!

### Contributor Metrics

![Surface](https://repobeats.axiom.co/api/embed/53b366be450dbb713efa2fee9e2f95abe2ded62e.svg "Repobeats analytics image")
