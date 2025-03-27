# Creating a custom conda environment for Jupyter notebook in SCG
Thank you to @chunerguo https://github.com/chunerguo/resources/blob/main/scg_conda_env.md

## Create a new conda environment in a non-default directory
`conda create -p /labs/delitto/james/.envs/jpa_infercnv python=3.12`

## Activate the conda environment
`conda activate /labs/delitto/james/.envs/jpa_infercnv`

## Install ipykernel
`conda install ipykernel`

## Install other packages, for example:
`pip install infercnvpy` # just did this for the jpa_infercnv environment. Including these other examples for reference only.
`conda install -c conda-forge scanpy python-igraph leidenalg`
`conda install scvi-tools -c conda-forge`

## Check GPU info
`nvidia-smi`

## Register kernel
`python -m ipykernel install --user --name=jpa_infercnv`

# How to completely remove a conda environment
`conda remove -p /labs/delitto/james/.envs/jpa_infercnv --all`



