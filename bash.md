# Bash cheat sheet for the Linux command line
## Loading modules
`module avail` list all available modules \
`q` to exit any big list \
`module load my_module` load a module \
`module unload my_module` unload a module 

## SCG
`checkquota` \
`get_compute_charges -a account -u user` display your charges for the month for a given account \
`~akkornel/checkquota` check quota in home directory, scg labs folder, and oak

## GPUs
`nvidia-smi` check the GPU specs

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
`seff <JOBID>

## Edit a file in vim text editor
`vim file_name` \
`i` to insert \
`Esc` key to stop editing \
`:wq` to exit vim

