# Creating a custom mamba environment for Jupyter notebook on SCG

Thank you to Chuner Guo! \
https://github.com/chunerguo/resources/blob/main/how_tos/scg_conda_env.md

For reference:
https://mamba.readthedocs.io/en/latest/user_guide/mamba.html \
https://github.com/conda-forge/miniforge \
https://decoupler-py.readthedocs.io/en/latest/installation.html

## Install mamba
### Check the system architecture
`uname -m` \
x86_64

### Download the installer from Miniforge
https://github.com/conda-forge/miniforge/ \
`wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"`

### Run the interactive installer to install mamba into your home directory (fastest for high I/O work)
`bash Miniforge3-$(uname)-$(uname -m).sh` \
Answer `yes` to 'Do you wish to updated your shell profile to automatically initialize conda?'

## Create a new mamba environment in a non-default directory with the python 3.12 and decoupler dependencies
`mamba create -p /labs/delitto/james/.envs/decoupler python=3.12 conda-forge::decoupler-py`

## Activate the conda environment
`mamba activate /labs/delitto/james/.envs/decoupler`

## Install ipykernel
`mamba install ipykernel`

## Install other packages if needed:

## Register kernel
`python -m ipykernel install --user --name=decoupler`

## Deactivate
`mamba deactivate`
