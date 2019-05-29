Selecting Repo and Revision
===========================

TODO

Config file sets repo to use

Full Repo (example, and simple exclusions)
==========================================

Paths are taken from the root of the specified repo

    /*


Specification Format
====================

See also: [Shrinkwrap Docs](https://cvmfs.readthedocs.io/en/stable/cpt-shrinkwrap.html#cernvm-fs-shrinkwrap-layout)

Specific file

    /lcg/releases/gcc/7.1.0/x86_64-centos7/setup.sh

Full directory tree

    /lcg/releases/ROOT/6.10.04-4c60e/x86_64-cenots7-gcc7-opt/*

Directory contents only

    ^/lcg/releases/*

Exclusion rule

    !/lcg/releases/uuid

Example for ROOT version 6.10 (~8.3 GB)

    /lcg/releases/ROOT/6.10.04-4c60e/x86_64-centos7-gcc7-opt/*
    /lcg/contrib/binutils/2.28/x86_64-centos7/lib/*
    /lcg/contrib/gcc/*
    /lcg/releases/gcc/*
    /lcg/releases/lcgenv/*

Dynamic Tracing
===============

Useful for building Shrinkwrap specs

Live tracing of events for a particular job

Future jobs might require different things, so YMMV

FUSE client
-----------

Enable via config option

    CVMFS_TRACEFILE=/tmp/cvmfs-trace-@fqrn@.log

The cvmfs user must have write permission to the target directory

The `@fqrn@` syntax ensures that the trace file is different for every repository.

Trace is buffered internally, so be sure to unmount or run

    cvmfs_talk tracebuffer flush

to flush events to disk

See also: [CVMFS Docs](https://cvmfs.readthedocs.io/en/stable/cpt-tracer.html)

Parrot
------

Parrot also supports tracing file accesses with the `--name-list` option

Does not require FUSE installation or changes to client config

Different format than CVMFS tracer
