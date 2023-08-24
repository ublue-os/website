# Local Testing

Use a Fedora Silverblue virtual machine to test your changes locally.

## On host

1. Create `/etc/containers/registries.conf.d/local.conf` with:

    ```ini
    [[registry]]
    location = "localhost:5000"
    insecure = true
    ```

2. Run a local registry

    ```bash
    podman run -d -p 5000:5000 --restart=always --name registry registry:2
    ```

3. Build

    ```bash
    podman build . -t <name>
    ```

    For [startingpoint](https://github.com/ublue-os/startingpoint) forks:

    ```bash
    podman build . --build-arg=FEDORA_MAJOR_VERSION=<fedora-version> --build-arg=BASE_IMAGE_URL=<base-image> --build-arg=RECIPE=./recipe.yml -t <name>
    ```

    Fill the `build-arg`s from your recipe, e.g. `fedora-version` = latest, `base-image` = ghcr.io/ublue-os/silverblue-main.

4. Push image

    ```bash
    podman push localhost/<name>:latest localhost:5000/<name>:latest
    ```

## Running off a local tarball

```bash
podman build -t oci-archive:/var/home/$USER/container.tar.gz .
rpm-ostree rebase ostree-unverified-image:oci-archive:/var/home/$USER/container.tar.gz
```

## In VM

1. Create `/etc/containers/registries.conf.d/local.conf` with:

    ```ini
    [[registry]]
    location = "<host IP>:5000"
    insecure = true
    ```

2. Rebase

    ```bash
    rpm-ostree rebase --reboot ostree-unverified-registry:<host IP>:5000/<name>:latest
    ```

3. Upgrade

    After rebasing once, just upgrade after pushing a new version with the same image name:

    ```bash
    rpm-ostree upgrade --reboot
    ```
