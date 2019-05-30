What is Shrinkwrap?
===================

The CernVM-FS Shrinkwrap utility provides a means of exporting CVMFS repositories.
These exports may consist of the complete repository or contain a curated subset of the repository.

The CernVM-FS shrinkwrap utility uses libcvmfs to export repositories to a POSIX file tree.
This file tree can then be packaged and exported in several different ways,
such as SquashFS, Docker layers, or TAR file.
The `cvmfs_shrinkwrap` utility supports multithreaded copying to increase throughput and a file specification to create a subset of a repository.

Use Cases
=========

The shrinkwrap utility is a stand-alone tool that exports a part of a CernVM-FS repository directory hierarchy to another file system.
This exported tree can then be re-packaged into a “fat image” for HPC systems,
or it can be used for benchmarks that exclude possible performance effects caused by the CernVM-FS client,
such as network accesses to populate the cache.

Compared to UnCVMFS and rsync
=============================

[unCVMFS](https://github.com/ic-hep/uncvmfs)
downloads an entire CVMFS repo to local disk.
Paths can be blacklisted from the resulting SquashFS image,
but the whole thing is downloaded.
unCVMFS reads catalogs to quickly gather metadata and update existing checkouts.

Alternatively, it's possible to simply use rsync on a mounted repo.
Copying out through FUSE prevents more efficient hard linking and updates.

