Config files
============

Shrinkwrap relies on libcvmfs config

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
1. Adjust to your site
2. Need to be provided for shrinkwrap
3. Important as libcvmfs does not support shared caches

See also: [CVMFS Configuration](https://cvmfs.readthedocs.io/en/stable/cpt-configure.html)

Unprivileged Operation
======================

libcvmfs can map UIDs and GIDs to the current (non-root) user

**Assume current UID=1000 and GID=100**

You can use the `id` command to get these

Add the following lines to the CVMFS config

    CVMFS_UID_MAP=uid.map
    CVMFS_UID_MAP=gid.map

Then create `uid.map` containing

    * 1000

and `gid.map` containing

    * 100


Keys
====

TODO
