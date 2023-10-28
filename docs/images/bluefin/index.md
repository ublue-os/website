# Bluefin

!!! Note "**This image is considered Beta**"

A familiar(ish) Ubuntu desktop for Fedora Silverblue. It strives to cover these three use cases:

- For users it provides a system as reliable as a Chromebook with near-zero maintenance, with the power of Ubuntu and Fedora fused together.
- For developers we endeavour to provide the best cloud-native developer experience by enabling easy consumption of the [industry's leading tools](https://landscape.cncf.io/card-mode?sort=stars). These are included in dedicated `bluefin-dx` and `bluefin-dx-nvidia` images.
- For gamers we strive to deliver a world-class gaming experience via Flathub or [bazzite-arch](https://github.com/ublue-os/bazzite-arch)

![bluefin-defaultish](https://github.com/ublue-os/website/assets/1264109/63c40f3f-3e56-4aac-af7c-6cdc3cf6af4d)


> "Evolution is a process of constant branching and expansion." - Stephen Jay Gould

- ### [projectbluefin.io](https://projectbluefin.io)
- ### [Announcement Blog Post](https://www.ypsidanger.com/announcing-project-bluefin/)

## Usage

1. Download and install [the ISO from here](https://github.com/ublue-os/main/releases/latest/):
   - Select "Install ublue-os/bluefin" from the menu.
     - Choose "Install bluefin:38" if you have an AMD or Intel GPU.
     - Choose "Install bluefin-nvidia:38" if you have an Nvidia GPU.
   - [Follow the rest of the installation instructions](https://ublue.it/installation/).

### Rebase

For existing Silverblue/Kinoite users **AMD/Intel GPU users only**:

!!! warning "Rebasing and Flatpaks

    Bluefin will prompt you to modify your Flatpak remotes and will remove the Fedora remote. Cancel out of the first-run wizard if you want to leave your Flatpak configuration unchanged. 

1. After you reboot you should [pin the working deployment](https://docs.fedoraproject.org/en-US/fedora-silverblue/faq/#_about_using_silverblue) so you can safely rollback.
2. Open a terminal and rebase the OS to this image:

Bluefin:

```bash
sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin:38
```

Bluefin Developer Experience:

```bash
sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-dx:38
```

**Nvidia GPU users only** 

1. Open a terminal and rebase the OS to this image:

    Bluefin:

    ```bash
    sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-nvidia:38
    ```

    Bluefin Developer Experience:

    ```bash
    sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin-dx-nvidia:38
    ```  
  
2. Reboot the system and you're done!

### Revert

To revert back run:

  ```bash
  sudo rpm-ostree rebase fedora:fedora/38/x86_64/silverblue
  ```

  Check the [Silverblue documentation](https://docs.fedoraproject.org/en-US/fedora-silverblue/) for instructions on how to use rpm-ostree.

  We build date tags as well, so if you want to rebase to a particular day's release you can use the version number and date to boot off of that specific image:
  
  ```bash
  sudo rpm-ostree rebase ostree-image-signed:docker://ghcr.io/ublue-os/bluefin:37-20230310
  ```

The `latest` tag will automatically point to the latest build.

## Features

**This image heavily utilizes _cloud-native concepts_.**

System updates are image-based and automatic. Applications are logically separated from the system by using Flatpaks, and the CLI experience is contained within OCI containers.

## For Users

- Ubuntu-like GNOME layout.
  - Includes the following GNOME Extensions:
    - Dash to Dock - for a more Unity-like dock
    - Appindicator - for tray-like icons in the top right corner
    - GSConnect - Integrate your mobile device with your desktop    
    - Blur my Shell - for that bling
- GNOME Software with [Flathub](https://flathub.org):
  - Use a familiar software center UI to install graphical software
- Built on top of the the [Universal Blue main image](https://github.com/ublue-os/main)
  - Extra udev rules for game controllers and [other devices](https://github.com/ublue-os/config) included out of the box
  - All multimedia codecs included
  - System designed for automatic staging of updates
    - If you've never used an image-based Linux before just use your computer normally
    - Don't overthink it, just shut your computer off when you're not using it
- [Starship](https://starship.rs) is enabled by default to give you a nice shell prompt
- [Solaar](https://github.com/pwr-Solaar/Solaar) - included for Logitech mouse management along with `libratbagd`
- [Tailscale](https://tailscale.com) - included for VPN along with `wireguard-tools`
- `zsh` and `fish` optional

### Roadmap and Future Features

- Fedora 38 will be the initial release and will be considered Beta.
- Fedora 39 is the target for an initial GA release.

These are currently unimplemented ideas that we plan on adding:

- Provide a `:lts` tag derived from CentOS Stream for a more enterprise-like cadence.
- More robust system management via Cockpit

### Applications

- Mozilla Firefox, Extension Manager, Libreoffice, DejaDup, FontDownloader, Flatseal, and the Celluloid Media Player.
- Core GNOME Applications installed from Flathub:
  - GNOME Calculator, Calendar, Characters, Connections, Contacts, Evince, Firmware, Logs, Maps, NautilusPreviewer, TextEditor, Weather, baobab, clocks, eog, and font-viewer.
- All applications installed per user instead of system wide, similar to openSUSE MicroOS. Thanks for the inspiration Team Green!

### Recommended Extensions

The authors recommend the following extensions if you'd like to round out your experience. Use the included "Extensions Manager" application to search for these extensions; everything you need to get them to run is already included:

<img src="https://user-images.githubusercontent.com/1264109/224862317-569d018f-a7be-4895-82ff-e2c67652a0ab.png" width="400">

!!! Note 
    Installing extensions via extensions.gnome.org won't work, the extensions must be installed via this application.

- [Tailscale Status](https://extensions.gnome.org/extension/5112/tailscale-status/) for VPN.

## Frequently Asked Questions

> What about codecs?

Everything you need is included. You will need to [configure Firefox for hardware acceleration](/guide/codecs/)

> How do I get my GNOME back to normal Fedora defaults?

You can turn off the Dash to Dock and appindicator extensions to get a more stock Fedora experience. 

We set the default dconf keys in `/etc/dconf/db/local`, removing those keys and updating the database will take you back to the fedora default:

```bash
sudo rm -f /etc/dconf/db/local.d/01-ublue
sudo dconf update
```

If you prefer a vanilla GNOME installation check out [silverblue-main](https://github.com/ublue-os/main) or [silverblue-nvidia](https://github.com/ublue-os/nvidia) for a more upstream experience.

> Starship is not for me, how do I disable it?

You can remove or comment the line below in `/etc/bashrc` to restore the default prompt.

```bash
eval "$(starship init bash)"
```

> Should I trust you?

This is all hosted, built, and pushed on GitHub. As far as if I'm a trustable fellow, here's my [bio](https://www.ypsidanger.com/about/). If you've made it this far, then hopefully you've come to the conclusion on how easy it would be to build all of this on your own trusted machinery. :smile:

### Contributor Metrics

![Bluefin](https://repobeats.axiom.co/api/embed/40b85b252bf6ea25eb90539d1adcea013ccae69a.svg "Repobeats analytics image")
