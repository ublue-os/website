# Microsoft Surface Images

From the [linux-surface project](https://github.com/linux-surface/linux-surface)

> These days, Linux supports a lot of devices out-of-the-box. As a matter of fact, this includes a good portion of the Microsoft Surface devices—for most parts at least. So why would you need a special kernel for Surface devices? In short, for the parts that are not supported upstream yet.

- [ublue-os/surface](https://github.com/ublue-os/surface) - repository for generating these images

## Changes

Like all Universal Blue images, hardware acceleration and codecs are [included out of the box](/guide/codecs) and the system strives for a zero-maintenance based approach.

- Replaces the stock Fedora kernel with the [Surface kernel](https://github.com/linux-surface/linux-surface/tree/master/pkg/fedora)
- Replaces `power-profiles-daemon` with `tlp`


## Additional Diagnostic Tools

- `just benchmark` - will run [stress-ng](https://github.com/ColinIanKing/stress-ng) for 1 minute
- [`powertop`](https://github.com/fenrus75/powertop) - allows you to monitor power consumption in real time

## How to Help

Open Source succeeds best when contributors come together to solve a problem. These are areas where contributions would be appreciated:

- Additional `tlp` configurations. The image is designed to allow shipping multiple power profiles; we just need to collect and curate a set that would be the most useful for people.
- Benchmarking tools. It would be nice to be able to run a continuous benchmark that exercises the laptop and can run unattended so that we can automate power testing.

We want to allow Linux users to share this knowledge and expertise with each other to fulfill the true potential of Surface devices. We'll [use science](https://www.youtube.com/watch?v=BABM3EUo990) and the wonders of modern automation to accomplish this!

## Instructions

### Fresh installs


### Rebasing from another image

If you're rebasing from another image follow these instructions!