# Installing Software

## `rpm-ostree`

`rpm-ostree` is the system package manager for immutable Fedora variants. Unlike on more traditional Linux desktops, on an immutable Linux distribution you probably shouldn't install everything directly onto your base system. The more liberally you use the system package manager, the more likely you are to run into some instability that affects your base operating system.

To install a single package (for example, `zsh`), run
```
sudo rpm-ostree install zsh
```

To install multiple packages (for example, various CLI text editors), run
```
sudo rpm-ostree install micro neovim helix
```

To apply the staged new staged image that includes your packages, reboot your computer. 

## Flatpak

Flatpak is the default way of installing GUI applications on immutable Fedora variants. [Flathub](https://flathub.org/) is the largest repository of Flatpak applications. On Fedora versions below 38, you might need to add the Flathub repository by running
```
flatpak remote-add --if-not-exists --user flathub https://flathub.org/repo/flathub.flatpakrepo
```

You can install Flatpaks using GNOME Softare or KDE Discover if you happen to be on one of those desktop environments.

You can also install Flatpaks (for example, `mpv`) from the CLI by running
```
flatpak install flathub io.mpv.Mpv
```

You can also browse [the Flathub website](https://flathub.org/) and when deciding you want to install something copy the proper command from the section "Manual Install" at the bottom of the page.

There should be a `.desktop` file for the application, so you can run it with your application launcher. You can also run Flatpaks (for example, `mpv`) from the CLI by running
```
flatpak run io.mpv.Mpv
```

## Toolbox

Toolboxes are little CLI podman containers that you can install anything into without it polluting your host system. Read more on [the dedicated page](/usersguide/toolbox).

## Fleek / Nix

[Fleek](https://getfleek.dev/) is a wrapper for [Nix](https://nixos.org/manual/nix/stable/) [home-manager](https://github.com/nix-community/home-manager) that can be used to easily install different packages with Nix. The packages are not isolated or containerized in any way, but they are still not part of your base system, as they are installed into Nix-specific directories. 
Fleek & home-manager also take over some of your dotfiles such as your `.zshrc` or `.bashrc`.

To install a package (for example, `micro`) with Fleek, run
```
fleek add -a micro
```
The `-a` flag will apply the changes immediately, omitting it will just edit your configuration file and wait until you run `fleek apply` to apply it.

Read [the Fleek docs](https://getfleek.dev/) for more information.
