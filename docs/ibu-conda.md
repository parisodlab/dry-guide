# Using conda on IBU

[TOC]

## Why Conda

__Computational Reproducibility__ ensures that an analysis can be exactly replicated. To achieve this in computational research, it is essential to track the code, software, and data used. Code is managed using git and GitHub (refer to the [Github page](github.md) for assistance). Typically, the initial data (often FASTQs) remains unchanged, so tracking data changes is unnecessary. New analyses are conducted when additional data is introduced. Software, however, is updated frequently, and the same version of software may not be the latest in the future.

To track software, package and environment managers such as Conda and Singularity/Docker are very useful. 


## Setting up Conda on IBU

Anaconda is a Python distribution that contains many packages including conda. Miniconda is a more compact version of Anaconda that also includes conda. So in order to install conda, we usually either install Miniconda or Anaconda. On IBU, Anaconda is already installed. However there are many versions of Anaconda, each can have a different version of Python and Conda. The current environments at IBU is available using `module load Anaconda3/2022.05` (See **Notes** below for more info) You can check the availability in future using the command `module avail |& grep -i conda`.	

In your home directory `~/`, create a file called `.condarc` and put the following lines into it. It sets the channel priority when conda searches for packages. If possible, in one environment it is good to use packages from the same channel. 

```
channels:
  - conda-forge
  - bioconda
  - defaults
  
auto_activate_base: false

envs_dirs:
  - ~/.conda/envs/
  - /data/users/<user_id>/conda_envs/
```

## Using Conda

__[Conda Documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/index.html)__

__[Conda Cheatsheet](https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf)__

After loading the Anaconda module, one can create an environment and install packages into that environment:

```
# Create conda environment named "name_of_env"
conda create --name name_of_env

# Create conda environment in a specific folder
conda create -p /data/users/<user_id>/conda_envs/test

# activate conda environment
# for some `conda activate` works and for others `source activate`
conda activate test
source activate test

# install package into conda environment
conda install bcftools
```

When looking to install a package, one resource to check out is [anaconda.org](https://anaconda.org), search for your package and run the install command listed on the page.

!!! Note
	Remember to keep in mind the different versions of software/packages. You could have bcftools-v1.10 or bcftools-v.1.12, so make sure you install the correct one!

!!! Important
	You can also install R packages with conda, however conda and R don't always work well together. Check out our quick fix [here](r.md)

## Running Snakemake with conda

When running Snakemake, Conda environments should be stored in a subfolder `workflow/envs` (make sure to keep them as finegrained as possible to improve transparency and maintainability) (check out the [documentation](https://snakemake.readthedocs.io/en/stable/snakefiles/deployment.html#integrated-package-management)):


**Conda within a rule:**

```
rule NAME:
    input:
        "table.txt"
    output:
        "plots/myplot.pdf"
    conda:
        "envs/ggplot.yaml"
    script:
        "scripts/plot-stuff.R"
```


**Conda environment `snake_env.yaml` for the entire workflow: (with snakemake for execution working great in 2024)**

```
name: snake_env
channels:
    - conda-forge
    - bioconda
    - defaults
    - R
dependencies:
    - r-base=4.3.2
    - snakemake=8.16.0
    - snakemake-minimal=8.16.0
    - snakemake-wrapper-utils=0.1.3
    - pigz=2.3.4
    - toposort=1.10
    - python>=3.10
    - pip=23.1.2
# bioconda channel installs
    - fastqc
    - trimmomatic=0.36
    - multiqc
    - qualimap
    - pip:
        - snakemake-executor-plugin-cluster-generic
```

## Notes on conda versions on IBU

As of 2024, conda environments generated with `module load anaconda3/2022.05` from IBU loads Python version 3.9.12 and conda 4.12.0. 

Once you activate an environment with `conda activate env_name` or `source activate env_name`, the default conda usually get re-directed to the conda that were originally used to create the environment. This is good because it helps ensure that all packages in the same environment uses the same version of conda. One can go to `cd ~/.conda/env_name/bin` and `readlink -f conda` or `readlink -f activate` to see which version of conda is used by this environment. This is exactly how Snakemake determines which conda to use when using an existing conda environment. 

## A faster alternative to Conda

In recent years, a 'drop-in' replacement for Conda, called Mamba, was released. Mamba is faster at resolving dependencies, which improves wait times for creating and activating environments. Conda and Mamba seem to be forward and backwards compatible, and they share the same command structure. For example, `conda create` and `mamba create` do the same task and share the same parameters.

If you prefer to use Mamba, you can install it in your home directory by running these commands:

```
cd ~
wget https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh
chmod +x ./Mambaforge-Linux-x86_64.sh
./Mambaforge-Linux-x86_64.sh
```

After completing the installation, the `mamba` binary should be added to `$PATH`, and you should be able to create, configure, and activate environments using the same commands as `conda` (FYI the `conda` binary will still be available to be called from `$PATH` by default). 

You will immediately notice a difference in speed when using mamba. Test it by loading an environment:
```
mamba activate /data/users/<user_id>/conda_envs/<env_name>
```
