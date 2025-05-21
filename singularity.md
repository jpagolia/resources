# How to install and run a Docker container using Singularity on SCG
https://www.sherlock.stanford.edu/docs/software/containers/singularity/#importing-containers \
Thank you Chuner Guo! https://github.com/chunerguo/resources/blob/main/how_tos/scg_singularity.md

## Request an interactive shell with adequate resources
`sdev -c 4 -m 64 -t 04:00:00`

## Set up folders for the temp directory and cache that have no memory limit
`export SINGULARITY_TMPDIR='/labs/delitto/james/.envs/tmp_singularity/'` \
`export SINGULARITY_CACHEDIR=/labs/delitto/james/.envs/cache_singularity/` \
Note: make sure you have a trailing `/`, and use quotes for the path; otherwise this will not work. \
Alternatively, you can put these lines at the end of your .bashrc file, which is located in your home directory, then run `source ~/.bashrc`.

## Check that these assignments worked
`echo $SINGULARITY_TMPDIR` \
`echo $SINGULARITY_CACHEDIR`

## Pull the docker image
Change directory to the directory you want to put the image into with `cd <YOUR_DIRECTORY>`
`singularity pull docker://ghcr.io/genentech/scimilarity:latest &&singularity cache clean`

