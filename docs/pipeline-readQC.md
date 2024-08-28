# trim.rules

[TOC]

The [trim.rules](https://github.com/parisodlab/snakeGATK4_v2/blob/main/workflow/trim.rules) workflow performs FASTQ trimming to remove poor quality sequences and technical sequences such as adapters. It should be used with high-coverage genomic DNA.  
The pipeline contains the rules for trimming fastq files using Trimmomatic in a Snakemake workflow.  

The rules in this file perform the following tasks:
- Import necessary libraries and modules
- Read the configuration file
- Define wildcard constraints for prefixes and samples
- Define a function to get the fastq files for a given prefix
- Define a function to get the trimmed fastq files for a given prefix
- Define the 'trim' rule which specifies the input, output, log, benchmark, parameters, and wrapper for the Trimmomatic tool



# Pipeline overview

![Pipeline-overview](img/trim.rule.drawio.svg)

* You have downloaded FASTQ Data to a subdirectory within a data directory. 
* You have filled out the `config_main.yaml` file with the appropriate information.
* You have installed base snakemake environment using `conda env create -f envs/snake_env.yaml` and activated it using `conda activate snake_env`

# Usage

## Testing the pipeline on IBU

*This command uses a test dataset*

```
snakemake -np -s workflow/trim.rules --profile slurm 2>&1 | tee logs/log_trim.txt
```

## Running the pipeline on IBU

*Note: if you are having issues running Snakemake or need reminders, check out the [Snakemake](ibu-snakemake.md) page.*

```
snakemake -s workflow/trim.rules --profile slurm 2>&1 | tee logs/log_trim.txt
```

