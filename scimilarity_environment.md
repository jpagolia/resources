# Create a conda environment for Scimilarity
See these instructions: https://genentech.github.io/scimilarity/install.html

## Download yaml file
environment.yaml

# Navigate to directory
`cd /labs/delitto/james/.envs/` and upload environment.yaml

## Create a conda environment from a yaml file like this:
`conda env create -f environment.yaml`

## Activate the conda environment
`conda activate scimilarity`

## Install scimilarity
`pip install scimilarity`

## Register kernel
`python -m ipykernel install --user --name=scimilarity`

## Deactivate
`conda deactivate`
