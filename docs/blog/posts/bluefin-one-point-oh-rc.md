---
date: 2023-10-23
comments: true
authors: 
  - castrojo
categories:
  - bluefin
links:
  - Bazzite: https://github.com/ublue-os/bluefin
  
---

# Bluefin is on it's way to Beta

After nearly two(!) years of prototyping and testing, [Bluefin](/images/bluefin) is on it's way to Beta! We're hoping to do the final release of the beta on November 1st, so we'd like to spend a some time testing the ISO. 

Bluefin is an interpretation of the Ubuntu spirit built with Fedora technology. It's a familiar(ish) Ubuntu desktop for Fedora Silverblue. It strives to cover these three use cases:

- For users it provides a system as reliable as a Chromebook with near-zero maintenance, with the power of Ubuntu and Fedora fused together.
- For developers we endeavour to provide the best cloud-native developer experience by enabling easy consumption of the [industry's leading tools](https://landscape.cncf.io/card-mode?sort=stars). These are included in dedicated `bluefin-dx` and `bluefin-dx-nvidia` images.
- For gamers we strive to deliver a world-class gaming experience via Flathub or [bazzite-arch](https://github.com/ublue-os/bazzite-arch)
 
**A good internet connection is required.**

## [bluefin-38-2023-10-23-x86_64.iso](https://ublue.download/bluefin-38-2023-10-23-x86_64-rc.iso)

### Instructions

- Follow the [installation instructions](/installation/) for current known issues:
  - Dual boot configurations are not supported
  - Manual partitioning is not suppported.
  - Installation progress will appear to have stalled but is progressing in the background 
  - Applications like Firefox and other core apps will be installed on login, this might take a while depending on your internet connection speed. The system will notify you when it is completed:

![image](https://github.com/ublue-os/bluefin/assets/1264109/6611b898-e8f0-46b0-ab0e-ddf8b5709c42)

## Thanks!

Special thanks to [akdev1l](https://github.com/akdev1l/), [bobslept](https://github.com/bobslept), and [gerblesh](https://github.com/gerblesh) for their hard work over the past few weeks to make this happen. 
