# Sequencing Example 

Genome sequencing via NGSEP is the emphasis here. As it is relatively small (i.e., a small eukaryote), use will be made of yeast. Yeast data of interest has been acquired from a standard repository [NCBI](https://www.ncbi.nlm.nih.gov). It will be compared with _Saccharomyces cerevisiae_ as the reference genome from [an NGSEP repository](https://sourceforge.net/projects/ngsep/files/training/). For the purposes of this module, both sets of data have been acquired and made available via blob storage on Azure. 

> **Note:** 
> Acquiring the yeast data from NCBI involves use of a 'download tool' known as [the SRA Toolkit](https://www.ncbi.nlm.nih.gov/home/tools/). As the Genomics Analysis module makes use of a virtual machine (VM) running Linux, use of this download tool is covered there.   

Genome sequencing begins by mapping reads via the `ReadsAligner` command of NGSEP as follows:

<!--->
correct paths - account for blob storage 
explain mapping reads 
<--->

```bash
java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/ER7A_1.fastq.gz -i2 ../reads/ER7A_2.fastq.gz -s ER7A -o ER7A.bam >& ER7A_aln.log
```

<!--->
log file needed? 
<--->

The rest of the input to NGSEP can be delineated as follows:

- The reference genome - indicated by the `-r` flag, this reference is _Saccharomyces cerevisiae_ detailed in FASTA format
- Inputs of interest - split across two FASTQ format files, and indicated by the `-i` flags, the ER7A parental strain are provided as input from Azure blob storage 
- Sample identifier - indicated by the `-s` flag, `ER7A` is the sample identifier 
- Output -  indicated by the `-o` flag is the name of the output file with the aligned reads in BAM format 
- Redirected standard output - redirected as indicated above, standard output and standard error are stored in a log file 

> **Note:**
> NGSEP documentation is available [here](https://sourceforge.net/projects/ngsep/files/Library/). Search for `ReadsAligner` to obtain the details of the options and arguments available for this NGSEP command. 

Copy and paste the above NGSEP `ReadsAligner` command into the "command line" field. Click on `Submit`. 

The Azure Batch task you've created will take some time to run - approximately 15 minutes on one of the compute nodes. 

<!--->
need to verify 
<--->

The output of NGSEP's `ReadsAligner` will be available via Azure Batch. The binary-format output (i.e., the BAM file) for the ER7A parental strain will be written as output to Azure blob storage. 

The sample of interest includes a second strain. Thus, the same NGSEP command needs to be re-run against this strain as follows:

```bash
java -jar ~/academy/bin/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/CBS4C_1.fastq.gz -i2 ../reads/CBS4C_2.fastq.gz -s CBS4C -o CBS4C.bam >& CBS4C_aln.log 
```

The details of the NGSEP options and arguments are analogous to the delineation provided previously. 

```bash
java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_ER7A I=ER7A.bam O=ER7A_sorted.bam >& ER7A_sort.log
```