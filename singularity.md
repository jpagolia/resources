# How to install and run a Docker container using Singularity on SCG
https://www.sherlock.stanford.edu/docs/software/containers/singularity/#importing-containers \
Thank you Chuner Guo! https://github.com/chunerguo/resources/blob/main/how_tos/scg_singularity.md

## Tmux and request an interactive shell with adequate resources
`tmux new -s <SESSION_NAME>` \
`sdev -c 2 -m 64 -t 12:00:00`

## Set up folders for the temp directory and cache that have no memory limit
`export SINGULARITY_TMPDIR='/oak/stanford/groups/longaker/james/tmp_singularity/'` \
`export SINGULARITY_CACHEDIR='/oak/stanford/groups/longaker/james/cache_singularity/'` \
Note: make sure you have a trailing `/`, and use quotes for the path; otherwise this will not work. \
Alternatively, you can put these lines at the end of your .bashrc file, which is located in your home directory, then run `source ~/.bashrc`.

## Check that these assignments worked
`echo $SINGULARITY_TMPDIR` \
`echo $SINGULARITY_CACHEDIR`

## Pull the docker image
Change directory to the directory you want to put the image into with `cd <YOUR_DIRECTORY>`
`singularity pull docker://ghcr.io/genentech/scimilarity:latest && singularity cache clean` This will also clean the cache after you are done.

## Download the trained models and weights
`wget https://zenodo.org/records/10685499/files/model_v1.1.tar.gz`

## Run the image and install ipykernel
"We require binding /models to your local path storing SCimilarity models, /data to your repository of scRNA-seq data, and /workspace to your notebook path." \
```
singularity exec --bind /oak/stanford/groups/longaker/ULMS/redo_analysis/code/:/workspace \
                 --bind /oak/stanford/groups/longaker/ULMS/redo_analysis/objects/:/data \
                 --bind /oak/stanford/groups/longaker/ULMS/james/scimilarity/:/models \
                 ./scimilarity_latest.sif start-notebook` \
```
`python -m ipykernel install --user --name=scim_env`

##

