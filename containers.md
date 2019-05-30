Image/archive files
===================

SquashFS is the simplest to build

    mksquashfs /PATH/TO/IMG img.squashfs

Tarballs are also straightforward

    tar -cfz img.tar.gz /PATH/TO/IMG

Containers
==========

Common container systems include
[Docker](https://www.docker.com/)
(likely not available in HPC settings),
[Singularity](https://www.sylabs.io/singularity/),
[Shifter](https://docs.nersc.gov/programming/shifter/how-to-use/).

NERSC uses Shifter for Docker-like experience in HPC.
Shifter can import Docker containers and image files.

For Docker, etc. there are two general options:
- bind mount a CVMFS checkout into the container
- burn the CVMFS tree into an image or layer

These come with the trade offs you might expect:
externally mounted repo isn't included in `docker push`/`pull`,
but there's an extra copying step with the image/layer.

(more detail about Docker volumes)

Similar steps for Singularity:

(insert details)

Shifter also supports
[volume mounts](https://docs.nersc.gov/programming/shifter/how-to-use/#volume-mounting-in-shifter).

(details)

