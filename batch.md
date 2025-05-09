# How to run a batch python script

First, write your python script in jupyter notebook and save it as a .ipynb file.
Then, do this to convert it to a .py script:\
`module load jupyter`\
`jupyter nbconvert --to python my_notebook.ipynb`

Next, create a .sh file for SLURM, which is job manager. The .sh file should be saved with the .sh file extension.
If you are using your virtual environment, it should look like this. You may have to cut and paste into notebook or type out yourself 
to get in the correct format.
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
If you are using a conda environment, use this. Notice the use of the gres command to request a GPU.
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
Save this file as an .sh file.\
Navigate to the directory you want to run the code in with\
`cd my_directory`
Then submit the job to SLURM with\
`sbatch my_sh_file.sh`
This is assuming that you submitted the job in the same directory as the .sh file. Otherwise, you will need to provide the file path.

To check on the status of your job, use\
`squeue -u my_username`

You will find a slurm output file in the directory in which you ran the code.
