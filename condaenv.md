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
`conda install -c conda-forge scanpy python-igraph leidenalg` # gave an error
`pip install -i https://test.pypi.org/simple/ "scikit-misc==0.2.0rc1"` # did not work
`pip install --user scikit-misc`

https://github.com/scverse/scanpy/issues/2073

## Check GPU info
`nvidia-smi`

## Register kernel
`python -m ipykernel install --user --name=jpa_infercnv`

# How to completely remove a conda environment
`conda remove -p /labs/delitto/james/.envs/jpa_infercnv --all`



