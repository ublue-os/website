---
date: 2023-05-19
authors: 
  - bsherman
  - castrojo
 
links:
  - Nvidia Instructions: https://github.com/ublue-os/nvidia#setup
---

# Important Secure Boot Changes required for Nvidia Image Users

As part of our move to beta we've found a scaling issue that needs to be sorted; skip below if you just want the instructions.

Initially the Nvidia images were signed by a key scoped only to the [ublue-os/nvidia repository](https://github.com/ublue-os/nvidia). At the time, we didn't expect to grow much past that, but now we want to add more akmods (like OBS loopback camera, XBox Wireless Controllers, etc.) which we are building in a seperate [ublue-os/akmods repository](https://github.com/ublue-os/akmods) as a "new layer" if you will. 

As part of our secrets management process, we are regenerating the keys used for Secure Boot signing our kernel modules. This means existing users must install a new key for all of Universal Blue akmods in addition to the key specific to Nvidia. 

On June 17th, we will switch Secure Boot signing to use the new key; from that time on only the new new key will be required.

As of this morning the new key is on the images, so subsequent new installations will be fine.

## Actions Needed

If you use Secure Boot with Nvidia you are likely on the outdated keys, you MUST run the following commands to add to the new key **BEFORE JUNE 17th**: 

    sudo mokutil --import /etc/pki/akmods/certs/akmods-ublue.der

Full instructions are [in the README](https://github.com/ublue-os/nvidia#setups) and we have [fresh ISOs](https://github.com/ublue-os/main/releases) as well if you're interested in helping to test.

New installations will not be affected after May 20th 2023. 

We apologize for the inconvenience that this may cause as we continue to improve our processes, thanks!
