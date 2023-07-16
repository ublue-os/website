# [`just`](https://just.systems)

`just` is a task runner similar to make, but designed to run project-specific commands, it's not a build system. This allows us to ship common aliases and scripts through one unified command. It can run scripts, accept command line arguments, and generally serve as a common tool for us to ship "custom commands" to users via a common framework. All Universal Blue images include `just` and `justfiles` with quality-of-life commands

## Example Commands

Typing `just` in the command line will show possible commands. Here are some common commands included in the Universal Blue images:

- `just bios` - boot into UEFI/bios. Useful for multiple boot systems
- `just changelogs` - show a changelog between the running system and the latest updates
- `just clean` - clean up old containers and packaging metadata
- `just distrobox-` - premade distroboxes of common distributions
- `just update` - update all packages, flatpaks, and distroboxes

### Nvidia Images

- `just set-kargs-nvidia` - set boot arguments to blacklist nouveau
- `just enroll-secure-boot-key-legacy-nvidia` - import boot key
- `just test-cuda`- test CUDA
- `just setup-firefox-flatpak-vaapi-nvidia` - set the flatpak override to get vaapi working

Commands are updated and maintained by the community, feel free to [submit a command](https://github.com/ublue-os/config/tree/main/build/ublue-os-just) if you feel it is something that would be useful for all users.

## Set up and configuration

`just` supports [include directives](https://just.systems/man/en/chapter_52.html) under the `--unstable` flag which is enabled by default with a shell alias set in `/etc/profile.d/`. If you have a posix-incomptable shell such as `fish`, you will need to alias `just` to `just --unstable` manually or wait until [`just` PR #1588](https://github.com/casey/just/pull/1588) merges, and you're able to set it as an environment variable instead.

`just` comes set up with Universal Blue images out of the box. There should be a `.justfile` in your home directory with the following contents: 

```just
!include /usr/share/ublue-os/just/main.just
!include /usr/share/ublue-os/just/nvidia.just
!include /usr/share/ublue-os/just/custom.just
```

- `main.just` is a `justfile` available in all `main` and derived images. It includes common system recipes such as `just update`.
- `nvidia.just` is a `justfile` available in all `nvidia` and derived images. It includes Nvidia-specifc recipes such as `just set-kargs-nvidia`.
- `custom.just` is a `justfile` available in `startingpoint` and derived images. It is intended to have recipes provided by the custom image maintainer.

You can inline more aliases in this file, or add custom includes. The included justfiles are there so that derived images can use the common community pattern while allowing extensibility.  

Then you can run `just` to list available recipes and `just recipename` to execute them. See [the `ublue-os-just` folder in the `config`-repo](https://github.com/ublue-os/config/tree/main/build/ublue-os-just) or just view the included `.just`-files for the source code of these recipes.

You can add custom recipes to the `justfile` in your home directory. [Read the documentation on proper syntax.](https://just.systems/man/en/chapter_18.html)
