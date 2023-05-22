# [`just`](https://just.systems)

`just` is a task runner similar to make, but only for running shell commands. All uBlue images include `just` and `justfiles` with QoL/system commands, such as `just update`, which updates the system, Flatpaks and distroboxes.

`just` supports [include directives](https://just.systems/man/en/chapter_52.html) under the `--unstable` flag which is enabled by default with a shell alias set in `/etc/profile.d/`. If you have a posix-incomptable shell such as `fish`, you will need to alias `just` to `just --unstable` manually or wait until [`just` PR #1588](https://github.com/casey/just/pull/1588) merges, and you're able to set it as an environment variable instead.

To get started using `just` on your system, create a `.justfile` in your home directory with the following contents.

```just
!include /usr/share/ublue-os/just/main.just
!include /usr/share/ublue-os/just/nvidia.just
!include /usr/share/ublue-os/just/custom.just
```

- `main.just` is a `justfile` available in all `main` and derived images. It includes common system recipes such as `just update`.
- `nvidia.just` is a `justfile` available in all `nvidia` and derived images. It includes Nvidia-specifc recipes such as `just set-kargs-nvidia`.
- `custom.just` is a `justfile` available in `startingpoint` and derived images. It is intended to have recipes provided by the custom image maintainer.

Then you can run `just` to list available recipes and `just recipename` to execute them. See [the `ublue-os-just` folder in the `config`-repo](https://github.com/ublue-os/config/tree/main/build/ublue-os-just) or just view the included `.just`-files for the source code of these recipes.

You can add custom recipes to the `justfile` in your home directory. [Read the documentation on proper syntax.](https://just.systems/man/en/chapter_18.html)
