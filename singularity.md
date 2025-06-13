# How to install and run a Docker container using Singularity on SCG
https://www.sherlock.stanford.edu/docs/software/containers/singularity/#importing-containers \
Thank you Chuner Guo! https://github.com/chunerguo/resources/blob/main/how_tos/scg_singularity.md

This example will show how to use Singularity to work with the Docker container for the python package Scimilarity: \
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
Change directory to the directory you want to put the image into with 
```
cd <YOUR_DIRECTORY>
singularity pull docker://ghcr.io/genentech/scimilarity:latest && singularity cache clean
```
This will also clean the cache after you are done.

## Download the trained models and weights
`wget https://zenodo.org/records/10685499/files/model_v1.1.tar.gz`

## Get a Singularity shell and install ipykernel
"We require binding /models to your local path storing SCimilarity models, /data to your repository of scRNA-seq data, and /workspace to your notebook path." \
So I put the model file, new python notebook file, and scimilarity image in the same directory and then go to that directory. Run the following command in that directory.
```
singularity shell --bind /oak/stanford/groups/longaker/james/scimilarity:/workspace \
                 --bind /oak/stanford/groups/longaker/ULMS/analysis_v3/objects:/data \
                 --bind /oak/stanford/groups/longaker/james/scimilarity:/models \
                 ./scimilarity_latest.sif
```
Install ipykernel with this command. This will create a kernel with the name `scim_env`. Customize your name as necessary. This will be included in the path to the `kernel.json` file below.
```
python -m ipykernel install --user --name=scim_env
```

To check where python is installed in this container, run `whereis python` or `which python` in the singularity shell. Alternatively, `import sys` and then `print(sys.executable)`.

## Step 3: modify kernel file
This `kernel.json` file will be run when you activate the jupyter kernel inside the singularity container.
Navigate to `~/.local/share/jupyter/kernels/scim_env/` and open the `kernel.json` file. Change the first few lines so that they look like this:

```
{
 "argv": [
  "/usr/bin/python", # this is the path to where python is installed inside the singularity container
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

## Run the image
Make sure you are in the directory where the scimilarity image (.sif file) is located. Then you can run this command to start a jupyter notebook.
```
singularity exec --bind /oak/stanford/groups/longaker/james/scimilarity:/workspace \
                 --bind /oak/stanford/groups/longaker/ULMS/analysis_v3/objects:/data \
                 --bind /oak/stanford/groups/longaker/james/scimilarity:/models \
                 ./scimilarity_latest.sif start-notebook
```
Building the SIF image file may take 10 minutes or so. Then, singularity will open a jupyter notebook and output two hyperlinks to it. To connect to the hyperlink through your computer, you will have to ssh into the correct local host and node running the singularity image, for example with the following command. This will change based on which node and which local host the notebook is running on, so check the output of your `singularity exec` command and modify the following command to match it.
```
ssh -L 8888:localhost:8888 <USERNAME>@smsh11dsu-srcf-d15-37.scg.stanford.edu
```
Then put the second URL that singularity spits out into your browser.

## Other tips and tricks
You can create the shell with the `--no-cleanup` option to avoid permissions issues with deleting files in the SINGULARITY_TMPDIR.
You can then `chmod -R u+rwx $SINGULARITY_TMPDIR` and `rm -rf` the tmp files, which have the prefix 'rootfs-'
