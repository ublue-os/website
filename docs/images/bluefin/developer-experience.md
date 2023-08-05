# bluefin-dx - The Bluefin Developer Experience

Dedicated developer image with bundled tools. It endevaours to be the world's most powerful cloud native developer environment. :) It includes everything in the base image plus: 

- [VSCode](https://code.visualstudio.com/) and related tools
- [virt-manager](https://virt-manager.org/) and associated tooling
- [Cockpit](https://cockpit-project.org/) for local and remote management 
- Podman and Docker extras
  - Automatically aliases the `docker` command to `podman`
  - podman.socket on by default so existing tools expecting a docker socket work out of the box
- LXC and LXD
- A collection of well curated monospace fonts 
- hashicorp repo included and enabled
  - None of them installed by default, but you can just add them to the Containerfile as you need them
- Built-in Ubuntu user space 
    - `Ctrl`-`Alt`-`u` - will launch an Ubuntu image inside a terminal via [Distrobox](https://github.com/89luca89/distrobox), your home directory will be transparently mounted
    - A [BlackBox terminal](https://www.omgubuntu.co.uk/2022/07/blackbox-gtk4-terminal-emulator-for-gnome) is used just for this configuration
    - Use this container for your typical CLI needs or to install software that is not available via Flatpak or Fedora
    - Optional [ubuntu-toolbox image](https://github.com/ublue-os/bluefin/pkgs/container/ubuntu-toolbox) with Python, and other convenience development tools. `just distrobox-bluefin` to get started. To configure `just` follow the [guide](https://ublue.it/guide/just/).
    - Optional [universal image](https://mcr.microsoft.com/en-us/product/devcontainers/universal/about) with Python, Node.js, JavaScript, TypeScript, C++, Java, C#, F#, .NET Core, PHP, Go, Ruby, and and Conda. `just distrobox-universal` to get started
    - `just assemble` shortcut to decleratively build distroboxes defined in `/etc/distrobox/distrobox.ini`
    - Refer to the [Distrobox documentation](https://distrobox.privatedns.org/#distrobox) for more information on using and configuring custom images
    - GNOME Terminal
      - `Ctrl`-`Alt`-`t` - will launch a host-level GNOME Terminal if you need to do host-level things in Fedora (you shouldn't need to do much).   
- Cloud Native Tools
    - [kind](https://kind.sigs.k8s.io/) - Run a Kubernetes cluster on your machine. Do a `kind create cluster` on the host to get started!
    - [kubectl](https://kubernetes.io/docs/reference/kubectl/) - Administer Kubernetes Clusters
    - helm, ko, flux, minio-client -- if it's an incubated project we intend to add it where appropriate
- [DevPod](https://devpod.sh/docs/what-is-devpod) - reproducible developer environments, powered by [devcontainers](https://containers.dev/) - Nix-powered Development Experience powered by Devbox
    - [Introducing Fleek](https://getfleek.dev)
      - `just nix-devbox` to get started
      - `just nix-devbox-global` to install a global profile
      - Check out [Devbox](https://www.jetpack.io/devbox) for more information
- Quality of Life Improvements
    - systemd shutdown timers adjusted to 15 seconds
    - [Tailscale](https://tailscale.com/) for VPN
    - [Just](https://github.com/casey/just) task runner for post-install automation tasks. Check out [our documentation](https://universal-blue.org/guide/just/) for more information on using and customizing just.
    - `fish` and `zsh` available as optional shells, use `just fish` or `just zsh` and follow the prompts to configure them