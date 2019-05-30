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

Bind Mounts
-----------

For a CVMFS repo checked out on the host machine, add

    --volume /PATH/TO/REPO:/cvmfs

Docker also supports named volumes to share data between containers.
In this case, Shrinkwrap would run *inside* a container.
See [Docker docs](https://docs.docker.com/storage/volumes/) for more info.

[Similar steps](https://www.sylabs.io/guides/3.2/user-guide/bind_paths_and_mounts.html)
for Singularity bind mounts.
If the administrator has enabled user-controlled bind mounts, add

    --bind /PATH/TO/REPO:/cvmfs

Shifter also supports
[bind mounting volumes](https://docs.nersc.gov/programming/shifter/how-to-use/#volume-mounting-in-shifter).
This time, we add to the submit script.

    #SBATCH --volume="/PATH/TO/REPO:/cvmfs"

Note that `$HOME`, `$SCRATCH`, etc. won't be resolved here,
so be sure to use full paths that are accessible from worker nodes.

Bundling (parts of) CVMFS in Container Images
---------------------------------------------

If you want to make the Shrinkwrap checkout part of the container build,
make sure `cvmfs-shrinkwrap` is already installed in the container and any keys or config files are prepared.
Then you can append to your Dockerfile

    RUN cvmfs_shrinkwrap --dest-base /cvmfs [...more options]

N.B. This could result in **long** `docker build` times.
Alternatively, you can copy an existing checkout from the host into a container layer.

    COPY --chown=cvmfs:cvmfs /PATH/TO/REPO /cvmfs

When updating, be sure to **rebuild the container** to avoid ballooning container sizes.
New layers don't delete data from older layers,
so appending rather than rebuilding brings *both* versions.


Singularity specifications can use the same two approaches.
To have Singularity run Shrinkwrap during container build,
add a line to your `%post` section

    %post
        ...
        cvmfs_shrinkwrap --dest-base /cvmfs [...more options]
        ...

For a checked out repo on the host machine,
you can have Singularity copy everything in via the `%files` section.

    %files
        /PATH/TO/REPO /cvmfs

Shifter and Singularity can import Docker images,
flattening them in the process.

    shifterimg -v pull docker:image_name:latest

or

    sudo singularity build lolcow.sif docker://godlovedc/lolcow

