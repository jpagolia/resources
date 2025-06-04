# Creating a custom mamba environment for Jupyter notebook on SCG

Thank you to Chuner Guo! \
https://github.com/chunerguo/resources/blob/main/how_tos/scg_conda_env.md

For reference:
https://mamba.readthedocs.io/en/latest/user_guide/mamba.html \
https://github.com/conda-forge/miniforge \
https://decoupler-py.readthedocs.io/en/latest/index.html

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

## Create a new mamba environment in a non-default directory with the python 3.12
`mamba create -p /labs/delitto/james/.envs/decoupler python=3.12`

## Activate the mamba environment
`mamba activate /labs/delitto/james/.envs/decoupler`

## Install ipykernel
`mamba install ipykernel`

## Install other packages if needed
Check which pip with `which pip` and make sure it is the pip in your mamba environment. Restart shell if not. \
`pip install decoupler==2.0.0` \
`pip install scanpy`

## Register kernel
`python -m ipykernel install --user --name=decoupler`

## Add optional dependencies as needed
`pip install marsilea` \
`pip install adjusttext` \
`pip install pydeseq2` \
`pip install igraph`

## Deactivate
`mamba deactivate`
