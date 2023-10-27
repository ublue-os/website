# Just

Just is a command runner.
In Bluefin it has default targets to make it easier to run common commands and perform system maintenance.
You can read more about [just in the upstream documentation](https://github.com/casey/just).

To list all available targets run `just -l`.
If you are in a directory with an existing `.justfile` or a `.justfile` exists in your file system tree that file will be used instead of `~/.justfile`.

### Just config
The default just config is stored in your home directory under `~/.justfile`.
```
cat ~/.justfile
```
You can add custom targets in this file.
To keep the system provided targets you need to include the line
```
!include /usr/share/ublue-os/justfile
```

### Update your system
To update your system including OS, flatpak, and distrobox containers run:
```
just update
```
This runs the following commands which you can see in `/usr/share/ublue-os/just/10-update.just`
```
rpm-ostree update
flatpak update -y
distrobox upgrade -a
```

### Install homebrew
To install homebrew run:
```
just brew
```
