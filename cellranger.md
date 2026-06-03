# Running cellranger on the command line on SCG

## check if fastqs are duplicates
- Do this for both fastqs to see if the first 20 lines are the same
```
zcat Undetermined_S0_L001_I1_001.fastq.gz | head -n 20
```
