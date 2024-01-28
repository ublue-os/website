# OStree

OStree is how the root filesystem in ublue is managed.
It can have multiple deployments including 1 active deployment and 1 or more standby or rollback deployments.
You can read more about [ostree](https://ostreedev.github.io/ostree/) in the upstream documentation.

## Managing ostree

### Update ostree
Pull updated version based on your current upstream repository.
```
rpm-ostree upgrade
```

### Roll back deployment
This will change your next target boot to the previous deployment.
Use this if you have issues with your current booted deployment.
```
rpm-ostree rollback
```

### Add rpm package
Install a new package layered on top of the file system tree.
Add `--now` to layer on top of the active tree.
```
rpm-ostree install $PACKAGE
```

### Get ostree status
See the current booted file system tree and any layered packages.
```
rpm-ostree status
```

### Pin a file system tree
To pin your current file system use `0` and for the previous booted file system use `1`.
This will keep a deployment available so it is not garbage collected.

Useful for major version changes and kernel changes.
```
sudo ostree admin pin 0
```
