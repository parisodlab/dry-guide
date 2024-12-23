# Introduction

[TOC]

The Parisod Lab makes use of IBU, the HPC at University of Bern. Take some time to read over the overview of what IBU is, what it does, how to use it, and how to sign up:

__[IBU Documentation](https://docs.pages.bioinformatics.unibe.ch/cluster-docs/)__

!!! Note
	New to the command line? Check out the [quick and dirty bash intro](bash.md) or [this introduction](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview) first!

## New Users

To gain access to IBU: 

Register new user by requesting IBU allocation and parisod group access to Pierre.
		
## Signing into IBU

After you gain access to the cluster you can login using:

```
ssh <user_id>@login8.hpc.binf.unibe.ch
```

To avoid typing in the password everytime, one can [set up a ssh key](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2).

If you are not familiar with what a bash profile is, [take a look at this](https://www.quora.com/What-is-bash_profile-and-what-is-its-use).

!!! Important
    When you login it is important to be conscientious of the fact that you are on a login node. You should not be running any sort of heavy duty operation on these nodes. Instead, any analysis you perform should be submitted as a job or run using an interactive job (see below).

## Login Nodes

When you login you will be assigned to a login node. .


## Home Directory

Logging in places you in your home directory. You can install software in your home directory for use when you run jobs, or for small files/analysis.

Your home directory has a quota of 50 Gb. You can quickly check the storage of your home directory (and any other storage attached to your user) using the following script:

```
lsquota
```

You can also check your storage space using the following command:

```
du -sh *
```

More information is provided below to help install and use software.

## Partitions/Queues

IBU has several partitions/queues where you can submit jobs. They have different computational resources, and are designed to run specific tasks that vary in complexity and runtime:

`pshort_el8`: This partition is designed to run quick jobs like tests, debugging, or interactive computing (Jupyter notebooks, R-Studio, etc). 

`pibu_el8`: This partition is designed to run a mix of jobs, from sequential jobs needing just one core to parallel jobs. Nodes on this queue may share resources with many other jobs. 


`pgpu`: This partition/queue is designed to run jobs that require the use of GPU nodes. The node has  2 Nvidia A100 gpus with 40GB  of memory per gpu. 

`phighmem`: This queue contains nodes with 2000GB of memory and it is designed to run jobs that require more than 192GB of memory. Use of this queue requires a separate allocation reIBU.


!!! Note
    The Allocation defines the user group access to these partitions. If you are not sure which partition to use, ask your PI or the IBU support team.

!!! Note
    Anyone who uses IBU should build your own project folder under `/data/projects/<project_number>/<user_id>` with your name. You should only write and revise files under your project folder. You can read/copy data from __p910__ but don't write any data out of your project folder. See the Storage section for more information.

!!! Important
	It is important that we keep the 120 Tb of storage space on **p910** from filling up with extraneous or intermediate files. It is good practice to clean up old data/files and backup important data at least every few months. You can check the percent of space remaining with `quotas.py`

## Request 'interact' sessions on IBU

If you are running a few simple commands or want to experiment with files directly you can start an interactive session on IBU. The command below (based on the `srun` command) will give you access to a node where you can run your command:

```
srun -p pibu_el8 -c 4 --mem 4G --time 2-0  --pty /bin/bash
```
Where `-c` is the number of cores,  `--mem` is the allocated memory,`-p` is the partition/queue, and `--time` is the walltime for the session.

!!! Important
    Do not run commands for big data directly on login node, they are not meant for running heavy-load workflows. Either open an interact session, or submit a job.

## Using `screen` or `nohup` to keep jobs from timing out

If you have ever tried to run a pipeline or script that takes a long time (think `snake_gatk`), you know that if you close down your terminal or if your IBU session logs out, it will cause your jobs to end prematurely. There are several ways to avoid this:

**screen**

Perhaps the most common way to deal with scripts that run for a long time is [`screen`](https://linuxize.com/post/how-to-use-linux-screen/). For the most simple case use, type `screen` to open a new screen session and then run your script like normal. Below are some more intermediate commands for taking full advantage of `screen`:

* `screen -R <some_descriptive_name>`: Use this command to name your screen session. Especially useful if you have several scren sessions running and/or want to get back to this particular one later.
* `Ctrl+a` follwed by `Ctrl+d` to detach from the current screen session (NOT `Ctrl+a+d`!)
* `exit` to end the current screen session
* `screen -ls` lists the IDs of all screen sessions currently running 
* `screen -R <screen_id>`: Use this command to resume a particular screen session. 

!!! Important
	When using `screen` on IBU, take note that screen sessions are only visible/available when you are logged on to the particular node it was created on. You can jump between nodes by simply typing ssh and the login node you want (_e.g._ `ssh login02`). 

**nohup**

Another way to avoid **SIGHUP** errors is to use [`nohup`](https://linuxhint.com/how_to_use_nohup_linux/). `nohup` is very simple to use, simply type `nohup` before your normal command and that's it!

```
nohup nextflow run main.nf 2>&1 &
``` 

Running a command with `nohup` will look a little different than usual because it will not print anything to the console. Instead, it prints all console outputs into a file in the current directory called `nohup.out`. You can redirect the output to another filename using:

```
nohup nextflow run main.nf > {date}_output.txt 2>&1 &
```

When you exit this window and open a new session, you can always look at the contents of the output file using `cat nohup.out` to see the progress.

!!! Note
	You can also run `nohup` in the background to continue using the same window for other processes by running `nohup nextflow run main.nf &`.
	By  2>&1 you are redirecting both stdout and stderr to the same file.
   
## Using packages already installed on IBU

IBU has a collection of packages installed. You can run `module avail |& less` or `module spider` to see what packages are currently available on IBU. You can use `module load bcftools` or `module load bcftools/1.15.1` to load packages with the default or a specific version (`module add` does the same thing). If you do `echo $PATH` before and after loading modules, you can see what module does is simply appending paths to the packages into your `$PATH` so the packages can be found in your environment.

`module purge` will remove all loaded packages and can be helpful to try when troubleshooting.

!!! Note
	You can also load/install software packages into conda environments for use with a specific project/pipeline. Check out the conda tutorial [here](ibu-conda.md).
   
## Submitting jobs to IBU

Jobs on IBU are managed by [SLURM](https://slurm.schedmd.com/). While most of our pipelines are managed by Nextflow, it is useful to know how to submit jobs directly to SLURM. Below is a template to submit an array job to SLURM that will run 10 parallel jobs. One can run it with `sbatch script.sh`. If you dig into the Nextflow working directory, you can see Nextflow actually generates such scripts and submits them to SLURM on your behalf. Thanks, Nextflow!

```
#!/bin/bash
#SBATCH -J name                # Name of job
#SBATCH -p pibu_el8            # Parition/Queue
#SBATCH -t 24:00:00            # Walltime/duration of the job (hh:mm:ss)
#SBATCH --cpus-per-task=1      # Number of cores (= processors = cpus) for each task
#SBATCH --mem-per-cpu=3G       # Memory per core needed for a job
#SBATCH --array=0-9            # number of parallel jobs to run counting from 0. Make sure to change this to match total number of files.

# make a list of all the files you want to process
# this script will run a parallel process for each file in this list
name_list=(*.bam)

# take the nth ($SLURM_ARRAY_TASK_ID-th) file in name_list
# don't change this line
Input=${name_list[$SLURM_ARRAY_TASK_ID]} 

# then do your operation on this file
Output=`echo $Input | sed 's/.bam/.sam/'`
```

## Monitoring SLURM Jobs on IBU

Here are some commmon commands used to interact with SLURM and check on job status. For more, check out [this page](https://slurm.schedmd.com/quickstart.html).

* `squeue -u <user_id>` to check all jobs of a user.

* `scancel <jobid>` to cancel a job. `scancel  {30000..32000}` to cancel a range of jobs (job id between 30000 and 32000).
