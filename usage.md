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

Rough Performance
=================

TODO

Efficient Updates
=================

On updates, new files are downloaded to the cache directory.
Updates are fast, as only changes need to be applied.

