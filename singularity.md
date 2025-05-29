# How to install and run a Docker container using Singularity on SCG
https://www.sherlock.stanford.edu/docs/software/containers/singularity/#importing-containers \
Thank you Chuner Guo! https://github.com/chunerguo/resources/blob/main/how_tos/scg_singularity.md

This is example will show how to use Singularity to work with the Docker container for the python package Scimilarity: \
https://genentech.github.io/scimilarity/install.html#using-the-scimilarity-docker-container

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

## Get a Singularity shell and install ipykernel
"We require binding /models to your local path storing SCimilarity models, /data to your repository of scRNA-seq data, and /workspace to your notebook path." \
So I put the model file, new python notebook file, and scimilarity image in the same directory and then go to that directory. Run the following command in that directory.
```
singularity shell --bind /oak/stanford/groups/longaker/james/scimilarity:/workspace \
                 --bind /oak/stanford/groups/longaker/ULMS/redo_analysis/objects:/data \
                 --bind /oak/stanford/groups/longaker/james/scimilarity:/models \
                 ./scimilarity_latest.sif
```
`python -m ipykernel install --user --name=scim_env`

## Step 3: modify kernel file

Now navigate to `~/.local/share/jupyter/kernels/scim_env/` and open the `kernel.json` file, which should look like:

```
{
 "argv": [
  "/usr/sbin/python",
  "-Xfrozen_modules=off",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "scim_env",
 "language": "python",
 "metadata": {
  "debugger": true
 }
}
```

In order for Jupyter to construct the kernel from the container when a notebook is started, you have to edit the `argv` key as follows. \
Make sure you repeat the bind statements to create the three required bind paths for the scimilarity package.

```js
{
 "argv": [
  "/usr/sbin/python",
  "exec",
  "--bind",
  "/oak/stanford/groups/longaker/james/scimilarity:/workspace",
  "--bind",
  "/oak/stanford/groups/longaker/ULMS/analysis_v3/objects:/data",
  "--bind",
  "/oak/stanford/groups/longaker/james/scimilarity:/models",
  "/oak/stanford/groups/longaker/james/scimilarity/scimilarity_latest.sif",
  "-Xfrozen_modules=off",
  "-m",
  "ipykernel_launcher",
  "-f",
  "{connection_file}"
 ],
 "display_name": "scim_env",
 "language": "python",
 "metadata": {
  "debugger": true
 }
}
```

The `scim_env` kernel should now be available when you start a Jupyter Notebook Server session on [SCG OnDemand](https://ondemand.scg.stanford.edu/).

## Run the image
Make sure you are in the directory where the scimilarity image (.sif file) is located.
```
singularity exec --bind /oak/stanford/groups/longaker/james/scimilarity:/workspace \
                 --bind /oak/stanford/groups/longaker/ULMS/analysis_v3/objects:/data \
                 --bind /oak/stanford/groups/longaker/james/scimilarity:/models \
                 ./scimilarity_latest.sif start-notebook
```

