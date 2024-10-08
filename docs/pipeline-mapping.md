# mapping.rules

[TOC]

The [mapping.rules](https://github.com/parisodlab/snakeGATK4_v2/blob/main/workflow/mapping.rules) pipeline performs alignment for paired end fastq sequence data __at the sample__, and outputs BAMs and related information. Those BAMs can be used for downstream analysis including [variant calling](http://parisodlab.github.io/dry-guide/pipeline-GATK/), [concordance analysis](http://parisodlab.github.io/dry-guide/pipeline-concordance/) and other analyses.  


This pipeline contains the rules for a SnakeMake workflow for mapping reads to a reference genome and performing various analyses on the mapped data.

The rules in this file include:
- `end`: A rule that specifies the input and output files for generating a multiqc report.
- `mapping`: A rule that maps the reads to the reference genome using BWA and generates a BAM file.
- `MergeBamLanes`: A rule that merges BAM files from different lanes into a single BAM file.
- `MarkDuplicates`: A rule that marks duplicate reads in the BAM file.
- `CoverageReport`: A rule that calculates coverage statistics from the deduplicated BAM file.
- `genomeCov`: A rule that generates a coverage file for the entire genome using the `bamcov` tool.
- `deeptoolsCov`: A rule that generates coverage statistics using the `plotCoverage` tool from the `deeptools` package.
- `goleftCov`: A rule that generates coverage statistics using the `goleft` tool.
- `samtoolsStats`: A rule that generates various statistics using the `samtools` package.
- `multiqcCoverage`: A rule that generates a multiqc report from the coverage statistics generated by the other rules.

Each rule specifies the input and output files, as well as any parameters and shell commands that need to be executed.


# Pipeline overview

![Pipeline-overview](img/mapping.rules.drawio.svg)

* You have checked the QC of the FASTQ data using the [readQC](pipeline-readQC.md) pipeline
* You have trimmed the FASTQ data using the [trimming](pipeline-trimming.md) pipeline if the read quality was poor based on the readQC pipeline. OR you have skipped trimming if the read quality was good and there we no remaining adapters.
* You have filled out the `config_main.yaml` file with the appropriate information.
* You have installed base snakemake environment using `conda env create -f envs/snake_env.yaml` and activated it using `conda activate snake_env`

# Usage

## Testing on IBU

*This command uses a test dataset*

```
snakemake --np -s workflow/mapping.rules --profile slurm 2>&1 | tee logs/log_map.txt
```

## Running on IBU

You should run this in a screen session.

*Note: if you are having issues running Snakemake or need reminders, check out the [Snakemake](ibu-snakemake.md) page.*

```
snakemake -s workflow/mapping.rules --profile slurm 2>&1 | tee logs/log_map.txt
```

