# Creating a custom conda environment for Jupyter notebook on SCG
Thank you to Chuner Guo: https://github.com/chunerguo/resources/blob/main/scg_conda_env.md

## Create a new conda environment in a non-default directory
`conda create -p /labs/delitto/james/.envs/jpa_infercnv python=3.12`

## Activate the conda environment
`conda activate /labs/delitto/james/.envs/jpa_infercnv`

## Install ipykernel
`conda install ipykernel`

## Install other packages, for example:
`conda install -c conda-forge scanpy python-igraph leidenalg` \
`pip install -U scvi-tools` \
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


# Other resources
https://carpentries-incubator.github.io/introduction-to-conda-for-data-scientists/02-working-with-environments/index.html

## Removing a conda environment
```
conda remove -p /path/to/your/env --all
```

## Installing a conda environment from yml file
https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#
```
conda env create -f environment.yaml -p /path/to/your/env
```
## These packages are easier to install with conda first:
  - pyarrow
  - h5py
  - imagecodecs
  - pyproj
In general, you should install as many packages/dependencies as you can through conda first, and then use pip to install anything unavailable through conda. This way, pip will use the conda-installed dependencies already in your environment. But conda will not use dependencies installed through pip, so installing through pip first and then adding stuff with conda will not work.
