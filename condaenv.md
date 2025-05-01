# Creating a custom conda environment for Jupyter notebook on SCG
Thank you to Chuner Guo: https://github.com/chunerguo/resources/blob/main/scg_conda_env.md

## Create a new conda environment in a non-default directory
`conda create -p /labs/delitto/james/.envs/jpa_infercnv python=3.12`

## Activate the conda environment
`conda activate /labs/delitto/james/.envs/jpa_infercnv`

## Install ipykernel
`conda install ipykernel`

## Install other packages, for example:
`conda install -c conda-forge scanpy python-igraph leidenalg`\
`pip install -U scvi-tools`\
`pip install infercnvpy`

## Due to a dependency issue with scikit-misc in scanpy
`pip install scikit-misc`

### Notes on dependency issue
https://github.com/scverse/scanpy/issues/2073\
https://github.com/scverse/scanpy/issues/3144

## Register kernel
`python -m ipykernel install --user --name=jpa_infercnv`

## Deactivate
conda deactivate

## Check GPU info to determine required cuda version for GPU use
`nvidia-smi`\
`module avail cuda`

## How to completely remove a conda environment
`conda remove -p /labs/delitto/james/.envs/jpa_infercnv --all`

## How to free up space from conda installation into home directory
`conda clean --all`

# Other resources
https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/02-working-with-environments/index.html

