# Mamba and JupyterLab on Linux
These instructions are not intended for beginners! 

Features of this setup are
1. mamba is used to manage both packages and environments (it is a dropin replacement for conda, just much faster)
1. The default and only channel configured for package downloads is conda-forge
1. Mamba bash autocompletion is still very limited (June 2023), so we just use standard conda Bash autocompletion
1. JupyterLab is only installed into the base environment
1. To enable the base environment to find any other environments, two things are necessary
    1. Package nb_conda_kernels *must* be installed in the base environment
    1. Package ipykernel *must* be installed in each of the other (non-base) environments
1. The base environment also includes support for plotly-express (which must be installed in each non-base environment)

Create the setup with this instructions
* Download mamba `wget "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-$(uname)-$(uname -m).sh -P ~/Downloads/"`
* Install mamba `bash ~/Downloads/Mambaforge-$(uname)-$(uname -m).sh` (yes to conda init)
* `source ~/.bashrc` <<-- **IMPORTANT**
* `conda config --set auto_activate_base false`
* `conda config --set channel_priority strict` in case channels other than conda-forge, are added in future
* `conda list` all packages should be from conda-forge channel
* `mamba update --all`
* `conda deactivate` to test
* `conda activate base`
* `mamba install conda-bash-completion`
* `conda deactivate`
* Edit ~/.bashrc to source the auto-completion scripts
```
    CONDA_ROOT=/home/brett/mambaforge
    if [[ -r $CONDA_ROOT/etc/profile.d/bash_completion.sh ]]; then
        source $CONDA_ROOT/etc/profile.d/bash_completion.sh
    fi
```
* `source ~/.bashrc` <<-- **IMPORTANT**
* `conda activate base` and test <TAB><TAB> auto-completion
* `conda deactivate`
* `mamba install --name base jupyterlab ipywidgets jupyter-dash nb_conda_kernels autopep8`
* `conda deactivate`
* `mamba create --name ds39 python=3.9 ipykernel numpy bottleneck numexpr pandas scipy scikit-learn matplotlib nbformat ploty_express autopep8`
* `conda activate base`
* `jupyter-lab` the Launcher tab will show all shortcuts to start notebooks from all environment found
