# Local Testing
Use a Fedora Silverblue virtual machine to test your changes locally.

### On host
1. Create `/etc/containers/registries.conf.d/local.conf` with:
```
[[registry]]
location = "localhost:5000"
insecure = true
```
2. Run a local registry
```
podman run -d -p 5000:5000 --restart=always --name registry registry:2
```
3. Build
```
podman build . -t <name>
```
For [startingpoint](https://github.com/ublue-os/startingpoint) forks:
```
podman build . --build-arg=FEDORA_MAJOR_VERSION=<fedora-version> --build-arg=BASE_IMAGE_URL=<base-image> --build-arg=RECIPE=./recipe.yml -t <name>
```
Fill the `build-arg`s from your recipe, e.g. `fedora-version` = latest, `base-image` = ghcr.io/ublue-os/silverblue-main.
4. Push image
```
podman push localhost/<name>:latest localhost:5000/<name>:latest
```

### In VM
5. Create `/etc/containers/registries.conf.d/local.conf` with:
```
[[registry]]
location = "<host IP>:5000"
insecure = true
```
6. Rebase
``` 
rpm-ostree rebase --reboot ostree-unverified-registry:<host IP>:5000/<name>:latest
```
