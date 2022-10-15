# Obtain & Prepare Unknown Samples 

## Set Up Your Workspace 

This module is derived from the [NGSEP Tutorial](https://sourceforge.net/projects/ngsep/files/training/Tutorial.txt/download). Accordingly, to set up your Workspace (i.e., your CentOS Linux based virtual machine), issue the following commands at the Bash shell prompt:

1. From your home directory, `mkdir -p academy/ngsep_tutorial`.
1. Move into the tutorial directory (`cd academy/ngsep_tutorial`) and make the following directories `mkdir mkdir reads reference mapping genotyping population`. Each of these will be used in subsequent sections of this module. 

## Obtain the SRA Tookit

To obtain the genomics data for the unknown yeast sample use is made of a toolkit. 

To obtain the SRA toolkit from [NCBI](https://www.ncbi.nlm.nih.gov/home/tools/):

1. `ssh` into your Linux VM - your Workspace for this module. 
1. At the Bash shell prompt, issue the command `mkdir -p academy/tools`.
1. Move into that newly created directory (`cd academy/tools/`).
1. Download the SRA toolkit from NCBI via the command `wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/3.0.0/sratoolkit.3.0.0-centos_linux64.tar.gz`. 
1. Restore the compressed archive with the command `tar -zxvf sratoolkit.3.0.0-centos_linux64.tar.gz`.
1. Move into the toolkit's newly created directory (`cd sratoolkit.3.0.0-centos_linux64`), and casually note its contents.
1. To configure the toolkit, issue the command `./bin/vdb-config --interactive`. Note that this command launches a curses-based interface (see below). Using your `<TAB>` key and/or letters, navigate to the `TOOLS` tab and select `current directory` by making use of the down arrow. Your selection should appear as below. Save your choice and exit. 

<!--- nest above? --->

![SRA toolkit configuration](https://raw.githubusercontent.com/ianl-terawe/academy/main/genomics/analysis/media/sra_config.png "SRA toolkit configuration")

> **Note:**
> Your Workspace is based on CentOS Linux. If you are making use of a different operating environment, download the appropriate version of the SRA toolkit from [here](https://www.ncbi.nlm.nih.gov/home/tools/). 

## Download the Genomics Data of Interest 

To obtain the yeast samples of unknown genetic details, work through these steps:

1. Make `reads` your working directory (`cd ~/academy/ngsep_tutorial/reads/`).
1. Configure the SRA toolkit. 
1. Initiate 'backgrounded downloads' of the samples by issuing the following two commands:

```bash
 ~/academy/tools/sratoolkit.3.0.0-centos_linux64/bin/fastq-dump --gzip --split-files SRR514834 & 
 ~/academy/tools/sratoolkit.3.0.0-centos_linux64/bin/fastq-dump --gzip --split-files SRR514835 & 
```

> **Note:**
> Downloading is _expected_ to take of order 20 minutes, as you are acquiring approximately 2 GB of data. While the downloads are active, `jobs -l` will their `Running` status. `ls -l` or `du -h *` indicates progress via file size.

_After_ the data has been successfully downloaded, change the names of the samples to human-friendly versions as follows:

```bash
mv SRR514834_1.fastq.gz ER7A_1.fastq.gz                                   
mv SRR514834_2.fastq.gz ER7A_2.fastq.gz
mv SRR514835_1.fastq.gz CBS4C_1.fastq.gz
mv SRR514835_2.fastq.gz CBS4C_2.fastq.gz
```

The unknown samples are ready for sequencing and analysis. 