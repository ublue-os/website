# Distrobox

Distrobox is an integrated container management option for creating semi-isolated environments.
By default distrobox containers have access to your home directory, devices, and can also be used for running GUI applications that are not packaged as Flatpak or AppImage.
You can read more about [distrobox in the upstream documentation](https://github.com/89luca89/distrobox).

## Create a distrobox
Distrobox comes with friendly `just` command runners.
You can create distrobox environments based on different Linux distros with `just distrobox-$DISTRO` commands.
```
just distrobox-ubuntu
```

## Enter a distrobox
You can execute a shell inside a distrobox environment with:
```
distrobox enter $NAME
```
You can see all the available distrobox containers with:
```
distrobox ls
```

## Export an application
If you install a GUI application inside a distrobox container you can use that application from your main system launcher by exporting the app.
To do that you will need to know the binary path to the application or the name of the application inside the system.

The export command needs to be run from inside a distrobox environment or executed with `distrobox-enter -n $NAME --`
```
distrobox-export --app $APP
```
or export a binary with
```
distrobox-export --bin /path/to/bin
```
By default an exported binary will have a script put in ~/.local/bin.
Make sure that is part of your `$PATH`

## Remove an exported application
To delete an exported application run the following command from within the distrobox container.
```
distrobox-export --delete --app $APP
```
