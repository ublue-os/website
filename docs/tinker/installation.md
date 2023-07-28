# Rebasing to your new signed custom image

The term "rebase" in this context means changing the core of your operating system from one image to another. To rebase to your custom image, you need to first have a system running system based on `rpm-ostree` such as Fedora Silverblue or any of the Universal Blue images.

!!! note

    In the commands below, replace `ublue-os/startingpoint` with `<username>/<imagename>`

First, run the command to rebase to the *unsigned* version of your image (ensuring the proper signing-related files are locally on your device):
```
sudo rpm-ostree rebase ostree-unverified-registry:ghcr.io/ublue-os/startingpoint:latest
```

Reboot to complete the rebase:
```
systemctl reboot
```

Then, rebase to the signed image:
```
sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/startingpoint:latest
```

And finally, reboot to complete the installation
```
systemctl reboot
```