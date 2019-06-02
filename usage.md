Invocation
==========

Assuming we have
- a [config file](setup.md) (`sft.cern.ch.config`)
- a [specification](spec.md) (`sft.cern.ch.spec`)
- [repo keys](setup.md)

Run Shrinkwrap as

    cvmfs_shrinkwrap \
        --repo sft.cern.ch \
        --src-config sft.cern.ch.config \
        --spec-file sft.cern.ch.spec \
        --dest-base $OUTDIR \
        --threads 16

Full set of available options:

    $ cvmfs_shrinkwrap --help
    CernVM File System Shrinkwrapper, version 2.6.0
    
    This tool takes a cvmfs repository and outputs
    to a destination files system.
    Usage: cvmfs_shrinkwrap [-r][-sbcf][-dxyz][-t][-jrg]
    Options:
     -r --repo        Repository name [required]
     -s --src-type    Source filesystem type [default:cvmfs]
     -b --src-base    Source base location [default:/cvmfs/]
     -c --src-cache   Source cache
     -f --src-config  Source config [default:cvmfs.conf:cvmfs.local]
     -d --dest-type   Dest filesystem type [default:posix]
     -x --dest-base   Dest base [default:/export/cvmfs]
     -y --dest-cache  Dest cache [default:$BASE/.data]
     -z --dest-config Dest config
     -t --spec-file   Specification file [default=$REPO.spec]
     -j --threads     Number of concurrent copy threads [default:2*CPUs]
     -p --stat-period Frequency of stat prints, 0 disables [default:10]
     -g --gc          Perform garbage collection on destination
