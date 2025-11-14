# Bash cheat sheet for the Linux command line
## Loading modules
`module avail` list all available modules \
`q` to exit any big list \
`module load my_module` load a module \
`module unload my_module` unload a module 

## SCG
`checkquota` \
`get_compute_charges -a account -u user` display your charges for the month for a given account \
`~akkornel/checkquota` check storage limit in home directory, scg labs folder, and oak \
`lfs quota -p 11432 /oak/stanford/ -h` show inodes (files) limit as well \
`du -sh *` check disk usage of all subdirectories and files in directory

## GPUs
`nvidia-smi` check the GPU specs. This will show the driver that is installed, as well as the cuda version needed. This must be done after sshing into the node that actually has the GPU attached to it, not the login node (which has a small GPU).
- You will need to install cuda into your virtual environment or conda environment, or load the cuda module if it is already installed somewhere else.
- You will also need to proper jax and jaxlib versions, as well as torch.
- https://login.scg.stanford.edu/tutorials/gpus/

## SLURM
`sbatch file_name.sh` submit a job \
`scancel <JOB_ID>` cancel a job \
`squeue -u <user_id>` see your job queue \
`squeue` see the whole queue \
`scontrol show job <JOB_ID>` see time limit and other status information about an ongoing job

## Check an an ongoing job
`ssh <node_id>` ssh into the node running your job. You can find which node this is using `checkquota -u <user_id>` \
`htop` gives you a list of the currently running jobs

## Check memory efficiency after a job is complete
`seff <JOBID>`

## Edit a file in vim text editor
`vim file_name` \
Use the arrow keys to move around. Mouse will not work. \
`i` to insert \
`Esc` key to stop editing \
`:wq` to exit vim

## Check what files are using a ton of memory - top 20 files or directories
`du -ah ~ | sort -rh | head -n 20` \
Showing hidden files and directories only: \
`du -ah ~/. | sort -rh | head -n 20`

## Get the current path
`pwd` \
Get the current path without sym links: \
`pwd -P`

## Deleting
Delete a file `rm <filename>` \
Delete a directory `rm -r <directory>` \
Delete all files in a directory `rm -rf <directory>`

## Loop through directories in bash
https://unix.stackexchange.com/questions/86722/how-do-i-loop-through-only-directories-in-bash

## Copy all files from a directory (and subdirectories within that directory) with a specific ending to a destination directory
```
# copy all .h5 files from one directory to another directory
find /original/directory -type f -iname "*.h5" -exec cp -t /dst/dir {} +
```

## Chaining commands together
```
Use ; to run commands sequentially regardless of success or failure.
Use && to run the second command only if the first command succeeds.
Use || to run the second command only if the first command fails.
```

## pip
- Clean cache: Make sure you are cleaning the right pip. So if you used pip to install within a conda environment, activate the conda environment first and then clean the cache with this command:
```
pip cache purge
```
- If issues building wheels, make sure GCC (GNU compiler) is loaded.
```
module load gcc
```
- Sometimes a recent PyPI release will break the pip wheel. If so, go back to the previous version x.x.x.
```
pip install PACKAGE_NAME==x.x.x
```
- If building from source, you can also try to load cmake:
```
module load cmake
```
- For pyarrow, it's better to install with conda.

## conda
- Clean cache
```
conda clean --all
```
- Remove package
```
conda remove <package>
```
- Remove an entire environment
```
conda remove -n <environment_name> --all
```
