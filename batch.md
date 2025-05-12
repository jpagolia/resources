# How to run a batch python script

1) First, write your python script in jupyter notebook and save it as a .ipynb file.
2) Then, do this to convert it to a .py script:\
`module load jupyter`\
`jupyter nbconvert --to python my_notebook.ipynb`

3) Next, create a .sh file for SLURM, which is the job manager that SCG users to prioritize and run submitted batch jobs. The .sh file should be saved with the .sh file extension.
If you are using a virtual environment, it should look like this. You may have to cut and paste into Notepad or type it out yourself 
to get it in the correct format. This .sh file is telling SLURM to run the following commands in an sh shell (or a bash shell).
```
#!/bin/sh
#SBATCH --job-name=name
#SBATCH --partition=batch
#SBATCH --time=24:00:00
#SBATCH --cpus-per-task=4
#SBATCH --mem=128GB
#SBATCH --account=delitto

echo "Start"

source /path_to_my_virtual_env/bin/activate

python my_notebook.py

deactivate

echo "Completion"
```
If you are using a conda environment, use this. Notice the use of the `gres` command to request a GPU.
```
#!/bin/bash
#SBATCH --job-name=scib
#SBATCH --partition=batch
#SBATCH --time=12:00:00
#SBATCH --cpus-per-task=4
#SBATCH --mem=128GB
#SBATCH --gres=gpu:1
#SBATCH --account=delitto

echo "Start"

eval "$(conda shell.bash hook)"

conda activate path_to_my_conda_env

python my_script.py

conda deactivate

echo "Completion"
```
Save this file as an .sh file.

4) Navigate to the directory you want to run the code in with\
`cd my_directory`

5) Then submit the job to SLURM with\
`sbatch my_sh_file.sh`\
This is assuming that you submitted the job in the same directory as the .sh file. Otherwise, you will need to provide the path to the .sh file.

6) To check on the status of your job, use\
`squeue -u my_username`

7) You will find a slurm output file with the .out extension in the directory in which you ran the code. This will contain all the output from the python notebook. Note that the python output is buffered, meaning that it prints in short batches once the output gets too big to hold in the buffer, not necessarily in real time (and sometimes may print out of order). If you want the output to be unbuffered, put:\
`export PYTHONUNBUFFERED=1`\
in your .sh file.

If you need to cancel the job for any reason, use:\
`scancel NUMERICAL_JOB_ID`

