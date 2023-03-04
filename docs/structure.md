# The inheritance structure of uBlue

uBlue is based on the rpm-ostree native container images hosted at [quay.io](https://quay.io/organization/fedora-ostree-desktops), based on the build scripts in the testing [repository](https://gitlab.com/fedora/ostree/ci-test). In the future, Fedora will likely provide the base container images in a more official fashion.

[ublue-os/main](https://github.com/ublue-os/main) is built from those basic images. It is an image containing the basic uBlue quality-of-life additions, such as automatic updates for the system and flatpaks, and some common packages used in downstream uBlue images.

The main image can be used directly, but if you own an Nvidia GPU and want to use the proprietary drivers, the [ublue-os/nvidia](https://github.com/ublue-os/nvidia) image includes everything the main image does, but adds the Nvidia drivers from RPMFusion without the need to actually have RPMFusion enabled on your system.

![Graph of the Ublue structure. Upstream Fedora images on the top, and only the opinionated main inherits from it. Users are on the bottom, and users get the Ublue main image, a hypothetical image intended for Amd gpus and another existing one for Nvidia gpus. A starting point image inherits from the main, Amd and Nvidia images, and it is inteded for further customization by tinkerers into community-built images.](ublue-structure-graph.png)
