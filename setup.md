Config files
============

Shrinkwrap relies on `libcvmfs` configuration file.

Example config for SFT:

    CVMFS_REPOSITORIES=sft.cern.ch
    CVMFS_REPOSITORY_NAME=sft.cern.ch
    CVMFS_CONFIG_REPOSITORY=cvmfs-config.cern.ch
    CVMFS_SERVER_URL='http://cvmfs-stratum-zero-hpc.cern.ch/cvmfs/sft.cern.ch'
    CVMFS_CACHE_BASE=/var/lib/cvmfs/shrinkwrap
    CVMFS_HTTP_PROXY=DIRECT                # 1
    CVMFS_KEYS_DIR=/etc/cvmfs/keys/cern.ch # 2
    CVMFS_SHARED_CACHE=no                  # 3
    CVMFS_USER=cvmfs

Notes:
1. Adjust to your site. Direct should only be used with no proxy available.
2. Need to be provided for Shrinkwrap. See below.
3. Important as `libcvmfs` does not support shared caches.

Since Shrinkwrap is using `libcvmfs`, many of the features of 
CVMFS using FUSE are available, with the exception of many 
caching features. 

See also: [CVMFS Configuration](https://cvmfs.readthedocs.io/en/stable/cpt-configure.html)

Unprivileged Operation
======================

CVMFS generally provides the UID and GID as a `cvmfs` user
or presents the UID and GID of the user who published the file.
This can cause permission errors for unprivileged users,
as the file creation attempts to preserve the information
and the UID and GID may not map correctly.
To avoid this
`libcvmfs` can map UIDs and GIDs to the current (non-root) user,
allowing the creating user control.

You can use the `id` command to get your UID and GID.

**Assume current UID=1000 and GID=100**

First create a UID map file named `uid.map` and add:

    * 1000

This will map any UID to `1000` in shrinkwrap.

Next a GID map file named `gid.map`. Add:

    * 100

This will similarly map any GID to `100` in shrinkwrap.

Finally, add the following lines to the CVMFS config, 
pointing to the newly created map files

    CVMFS_UID_MAP=uid.map
    CVMFS_UID_MAP=gid.map


See also: [CVMFS Configuration - File Ownership](https://cvmfs.readthedocs.io/en/stable/cpt-configure.html#file-ownership)

Keys
====

Keys are needed to access CVMFS repositories. 
Even though `libcvmfs` is unprivileged in user space, 
it still relies on keys to create a connection to CVMFS servers.
If you are using a system that already uses CVMFS, keys are generally located
at `/etc/cvmfs/keys/...`. 

The location of keys for Shrinkwrap, as noted above, should be reflected in the configuration.


