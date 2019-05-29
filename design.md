Architecture
============

TODO

Uses libcvmfs, copies out of cache

Aware of internal representation, so maintains dedup

Also writes provenance info

Notes
=====

Magic symlinks are resolved at image creation

Data store and filesystem tree need to be on the same filesystem (hard links)
