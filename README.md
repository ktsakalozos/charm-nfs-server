# Overview

This charm provides NFSv4 (http://nfs.sourceforge.net/). Installs and configures an NFSv4 daemon with the standard accompanying services, portmapd and idmapd.

# Usage

	juju deploy nfs

## Known Limitations and Issues

If you are attempting to deploy NFS to an LXC container, such as the juju local provider, there are additional steps that need to be taken prior to deploying the NFS charm.

On the LXC host:

	apt-get install nfs-common
	modprobe nfsd
	mount -t nfsd nfsd /proc/fs/nfsd

Edit /etc/apparmor.d/lxc/lxc-default and add the following three lines to it:

	mount fstype=nfs,
	mount fstype=nfs4,
        mount fstype=nfsd,
	mount fstype=rpc_pipefs,

after which:

	sudo /etc/init.d/apparmor restart

Finally:

	juju deploy nfs

# Contact Information

Konstantinos Tsakalozos <kos.tsakalozos@canonical.com>


## Upstream NFS Project

- To view the source: https://code.launchpad.net/~charmers/charms/precise/nfs/trunk
- To report a bug: https://bugs.launchpad.net/charms/precise/+source/nfs


## Acknowledgements

This charm is a fork of https://code.launchpad.net/~charmers/charms/trusty/nfs/trunk
