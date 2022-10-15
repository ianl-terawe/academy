# Obtain & Prepare Reference Genome 

## Obtain Data Regarding the Reference Genome 

Make `reference` your working directory (`cd ~/academy/ngsep_tutorial/reference/`).

The reference genome is yeast species _Saccharomyces_cerevisiae_. From the NGSEP training directory hosted by Sourceforge, obtain the four files that are named after this yeast species as follows:

1. `wget --no-check-certificate https://sourceforge.net/projects/ngsep/files/training/Saccharomyces_cerevisiae.fa/download` - the sequence in FASTA format 
1. `wget --no-check-certificate https://sourceforge.net/projects/ngsep/files/training/Saccharomyces_cerevisiae_STRs.txt/download` - STRs
1. `wget --no-check-certificate https://sourceforge.net/projects/ngsep/files/training/Saccharomyces_cerevisiae.gff3/download` - annotations in GFF3 format
1. `wget --no-check-certificate https://sourceforge.net/projects/ngsep/files/training/Saccharomyces_cerevisiae_repeats.txt/download`- repeats 

> **Note:**
> The `--no-check-certificate` option is required to bypass an expired certificate. 

As you work through this module, additonal context will be provided for each of the files above. 

## Prepare the Reference Data as Needed 

To obtain a list of sequences in the reference data, issue the command at the Bash shell prompt:

`awk '{ if(substr($1,1,1)==">") print substr($1,2) }' Saccharomyces_cerevisiae.fa > Saccharomyces_cerevisiae_seqNames.txt`

This file will prove useful when determining variants in a subsequent section. 

The reference genome is ready for use. 