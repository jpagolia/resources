# How to install and run a Docker container using Singularity on SCG
https://www.sherlock.stanford.edu/docs/software/containers/singularity/#importing-containers \
Thank you Chuner Guo! https://github.com/chunerguo/resources/blob/main/how_tos/scg_singularity.md

## Request an interactive shell with adequate resources
`sdev -c 4 -m 64 -t 04:00:00`

## Set up folders for the temp directory and cache that have no memory limit
`export SINGULARITY_TMPDIR=/labs/delitto/james/.envs/tmp_singularity`
`export SINGULARITY_CACHEDIR=/labs/delitto/james/.envs/cache_singularity`

