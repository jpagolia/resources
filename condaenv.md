#Creating a custom conda environment for Jupyter notebook in SCG

Thank you to @chunerguo https://github.com/chunerguo/resources/blob/main/scg_conda_env.md

##Create a new conda environment in a non-default directory
conda create -p /labs/delitto/james/.envs/jpa_infercnv python=3.12

##Activate the conda environment
conda activate /labs/delitto/james/.envs/jpa_infercnv

## Install ipykernel
conda install ipykernel


