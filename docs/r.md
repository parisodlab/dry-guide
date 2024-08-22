# R

[TOC]

## General R resources

If you are looking for some help getting started with R or taking your R to the next level, check out these useful resources:

* [Swirl - interactive R learning](https://swirlstats.com/students.html)
* [Tidyverse workshop and resources](https://github.com/katiesevans/nuit_tidyverse)
* [Parisod Lab R Knowledge base & Cheatsheet](https://github.com/Parisodlab/code_club/blob/main/R_cheatsheet.md)
* [R-bloggers - tips and tricks](https://www.r-bloggers.com/)
* [Using Rprojects to organize scripts](https://www.r-bloggers.com/2020/01/rstudio-projects-and-working-directories-a-beginners-guide/)
* [Using workflowR for reproducible work](https://www.rdocumentation.org/packages/workflowr/versions/0.7.0)
* [Using Rmarkdown to generate reports](https://rmarkdown.rstudio.com/articles_intro.html)
* Also check out the `lab_code` slack channel for help/ibuions!

## Using R on IBU

Making sure everyone has the same version of several different R packages (specifically Tidyverse) can be a nightmare for software development. Fortunately, there are several ways to get around this issue:

* __Docker/singularity container__ - instead of using conda environments (or maybe in addition to), a docker/singularity image can be generated with R packages installed. The benefit is that singularity images can be used on IBU or locally and minimal set up is required. The downside is that on some occasions there can be errors generating the docker image with incompatible package versions.

* __Library Paths__ - For several recent pipelines on IBU, we can get around using a docker container for R packages by installing the proper versions of R packages to a shared location (`/projects/b1059/software/R_lib_3.6.0`). With the following code, any lab member can load the R package version from that location when running the pipeline, causing no errors, even if they don't have the package installed in their local R. 

```
# to manually install a package to this specific folder
# make sure to first load the correct R version, our pipelines are currently using 3.6.0
module load R/3.6.0

# open R
R

# install package
install.packages("tidyverse", lib = "/projects/b1059/software/R_lib_3.6.0")

# if you load the package normally, it won't work (unless you also have it installed in your path)
library(tidyverse) # won't work

# load the package from the specific folder
library(tidyverse, lib.loc = "/projects/b1059/software/R_lib_3.6.0")

# or add the path to your local R library to make for easier loading
.libPaths(c("/projects/b1059/software/R_lib_3.6.0", .libPaths() ))
library(tidyverse) # works

# you can add the following lines to a nextflow script to use these R packages
# set a parameter for R library path in case it updates in the future
params.R_libpath = "/projects/b1059/software/R_lib_3.6.0"

# add the .libPaths to the top of the script dynamically (we don't want it statically in case someone wants to use the pipeline outside of ibu)
echo ".libPaths(c(\\"${params.R_libpath}\\", .libPaths() ))" | cat - ${workflow.projectDir}/bin/Script.R > Script.R
Rscript --vanilla Script.R

```

* __Using `renv` for R Package Management__: Renv is a package that allows you to create a project-specific library for R packages. This is useful for ensuring that all users have the same version of R packages. To use renv, you need to install the package and then run `renv::init()` in your R project. This will create a `renv.lock` file that lists all the packages you have installed in your project. When you share your project with someone else, they can run `renv::restore()` to install the same versions of the packages you have. This is a good way to ensure that everyone is using the same versions of R packages.

**Setting Up `renv`**: 

1. **Install `renv`**:
   First, you'll need to install `renv` if it isn't already installed.

   ```R
   install.packages("renv")
   ```

2. **Initialize `renv`**:
   Navigate to your project directory and initialize `renv`. This will create a project-specific library and an `renv.lock` file that captures the versions of the packages you are using.

   ```R
   renv::init()
   ```

   This will snapshot the current state of your R environment, saving the versions of all packages currently installed and used in the project.

3. **Install Packages**:
   You can install any required packages as usual, and `renv` will manage them within the project’s library.

   ```R
   renv::install("tidyverse")
   ```

4. **Snapshot Dependencies**:
   Whenever you make changes to your package dependencies, update the lock file to reflect these changes.

   ```R
   renv::snapshot()
   ```

   The `renv.lock` file can be committed to your version control system to ensure that anyone else using the project can recreate the exact same environment.

5. **Restoring the Environment**:
   When someone else clones your project repository, they can restore the project environment using the `renv.lock` file.

   ```R
   renv::restore()
   ```

   This will install the exact versions of the packages as specified in the `renv.lock` file, ensuring consistent environments across different users and systems.

**Using `renv` in Scripts and Pipelines**:

- You can add the following lines to your scripts to ensure the `renv` environment is automatically activated when running the script:

   ```R
   if (!requireNamespace("renv", quietly = TRUE)) install.packages("renv")
   renv::activate()
   ```

- For Nextflow pipelines, you can include `renv::activate()` at the beginning of your R scripts to make sure the correct environment is loaded:

   ```bash
   echo "renv::activate()" | cat - ${workflow.projectDir}/bin/Script.R > Script.R
   Rscript --vanilla Script.R
   ```

## Running Rstudio on IBU

The IBU Analytics Nodes allow users with active IBU allocations to use RStudio from a web browser. See [Research Computing: IBU Analytics Nodes](https://kb.northwestern.edu/ibu-rstudio) for an overview of the system.

Go to the [Rstudio browser](https://rstudio.ibuanalytics.northwestern.edu) (*make sure you are connected with VPN if you are off campus*). Log in with your netid and password just like you would on IBU.

!!! Note
	The version of R on the Rstudio browser is currently 4.1.1, which is likely different from the version of R you run on IBU. Therefore, you will need to re-install any packages you want to use in the browser.

You can set the working directory with `setwd("path_to_directory")` and then open and save files and data in Rstudio just like you were using it locally on your computer -- but with data and files on IBU!!


