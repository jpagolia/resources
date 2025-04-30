# Creating a conda environment for Cytotrace 2 on Stanford SCG cluster
https://github.com/digitalcytometry/cytotrace2/tree/main/cytotrace2_python \
https://docs.conda.io/projects/conda/en/stable/commands/create.html

## Clone github repository and navigate to the YAML file
`git clone https://github.com/digitalcytometry/cytotrace2` \
`cd cytotrace2/cytotrace2_python`

## Create environment from YAML file at new path
`conda env create --prefix /labs/delitto/james/.envs/cytotrace2-py -f environment_py.yml`

## Activate environment and install packages
`conda activate /labs/delitto/james/.envs/cytotrace2-py` \
`pip install .` \
`conda install -c conda-forge datatable`

`conda deactivate`
