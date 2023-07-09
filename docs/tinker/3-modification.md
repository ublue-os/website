# Modifying your custom image

Documentation for modifying images based on the [`ublue-os/startingpoint`](https://github.com/ublue-os/startingpoint) template resides inside the repository's README and as comments inside the `recipe.yml`. This page mostly serves as a collection of quick examples of common customizations.

## Changing the base image

In the `recipe.yml` set `base-image:` to the URL of the desired image without the protocol identifier such as `https://`. Find the list of images at [universal-blue.org/images](https://universal-blue.org/images/).

Example: Changing to `kinoite-nvidia`.
```yaml
base-image: ghcr.io/ublue-os/kinoite-nvidia
```

## Adding an RPM package

In the `recipe.yml` under the `rpm:` section there is a list of packages to `install:`. Add your desired packages there and commit.

Example: Adding `micro`.
```yaml
rpm:
  install:
    - micro
```