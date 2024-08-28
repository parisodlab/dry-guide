# Pipeline Overview

[TOC]

An overview of the sequencing pipelines is shown below. 

## SnakeGATK4_v2

!!! Note
	The full protocol (in development) can be found [here](https://github.com/parisodlab/snakeGATK4_v2/blob/main/README.md)

The main pipeline for a project involves quality control, trimming, mapping, and variant calling using GATK4.

Parameters:
    - config_main.yaml: YAML configuration file containing project details and workflow parameters.
    
Functions:
    - spend_time(start_time, end_time): Calculates the time spent between two given time points and returns it in the format "hours:minutes:seconds".

Workflow Steps:
1. Read the configuration file.
2. Check if quality control is required.
    - If yes, perform quality control using Snakemake and log the running time.
    - If no, check if trimming is required.
        - If yes, perform trimming using Snakemake and log the running time.
        - If no, skip trimming step.
3. Perform mapping using Snakemake and log the running time.
4. Perform variant calling using GATK4 using Snakemake and log the running time.

