# Setting Up a Toolbox

When you want to install applications not required on your base system and not available as Flatpaks, you can use a "toolbox" program. Toolbox programs run OS containers using [Podman](https://podman.io/) allowing you to enter into the containers' command line interfaces and use them transparently with access to files in your home directory. For example, you could have one toolbox where all of your software development-related packages and programs live.

Toolboxes don't require as much maintenance as running the distribution on bare metal, and you can very easily have multiple side-by-side, remove existing ones, and replace them with new entirely fresh ones.

Fedora comes with [`toolbx`](https://containertoolbx.org/) and the Universal Blue images come with both `toolbx` and [`distrobox`](https://distrobox.privatedns.org/), but this page will only cover `distrobox`.

## Creating and using a Distrobox

To create a Fedora 38 Distrobox, run:

```bash
distrobox create --image registry.fedoraproject.org/fedora-toolbox:38 --name fedora
```

To create an Ubuntu 22.04 Distrobox, run:

```bash
distrobox create --image docker.io/library/ubuntu:22.04 --name ubuntu
```

To create an Arch Linux Distrobox, run:

```bash
distrobox create --image docker.io/library/archlinux:latest --name arch
```

[List of tested container images](https://distrobox.privatedns.org/compatibility/#containers-distros).

When choosing an image for your container, consider which package manager and repos you want to use (e.g. `apt` vs. `pacman`), and pick one that you're most comfortable with!

Once you've created your Distrobox, you can enter it by running:

```bash
distrobox enter <boxname>
```

Now you have access to everything installed within the Distrobox and can install new packages using its package manager.

Read more in [the Distrobox documentation](https://distrobox.privatedns.org/) or [GitHub repository](https://github.com/89luca89/distrobox).

## Exporting programs from Distrobox

You can export a GUI program (for example, `mpv`) by running the following from **inside the Distrobox**:

```bash
distrobox-export --app mpv
```

You can also export a binary or CLI program (for example, `vim`) by running the following from **inside the Distrobox**. You need to provide an export path and know where the original binary exists in the Distrobox's filesystem. An easy way to find out is running `which vim` (replace `vim` with the name of the binary you want to export). The export command will create a shell script that runs the specified binary from inside the Distrobox.

```bash
distrobox-export --bin /usr/bin/vim --export-path ~/.local/bin
```

[Read more in the Distrobox documentation about `distrobox-export`](https://distrobox.privatedns.org/usage/distrobox-export/)

## Integrating VSCode with Distrobox

There are two ways to integrate VSCode with a Distrobox.  
The easiest way is to just install it inside your Distrobox and `distrobox-export` it. The integrated terminal and all addons will then be run inside that single Distrobox. The other way is with [the Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).
Both ways are detailed inside [the official Distrobox tutorial for integrating with VSCode](https://distrobox.privatedns.org/posts/integrate_vscode_distrobox/)

## Using the host's `xdg-open` inside Distrobox

Some GUI programs use `xdg-open` to open URLs, but it doesn't work when running your browser on the host.
You can fix this by adding the following shell script to your `~/.local/bin/` and giving it executable permissions.

```bash
#!/bin/bash
if [ ! -e /run/.containerenv ] && [ ! -e /.dockerenv ]; then # if not inside a container
    /usr/bin/xdg-open $@ # run xdg-open normally
else
	distrobox-host-exec /usr/bin/xdg-open $@ # run xdg-open on the host
fi
```

If you have `xdg-open` installed inside the Distrobox, you need to make sure that `~/.local/bin/` is in your `$PATH` before `/usr/bin/`.
