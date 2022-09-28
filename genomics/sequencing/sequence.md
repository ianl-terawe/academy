# Mapping Reads 

Genome sequencing via **NGSEP** is the emphasis here. As it is relatively small (i.e., a small [eukaryote](https://en.wikipedia.org/wiki/Eukaryote)), use will be made of yeast. Yeast data of interest has been acquired from a standard repository [NCBI](https://www.ncbi.nlm.nih.gov). It will be compared with _Saccharomyces cerevisiae_ as the reference genome from [an NGSEP repository](https://sourceforge.net/projects/ngsep/files/training/). For the purposes of this module, both sets of data have been acquired and made available via blob storage on Azure. 

> **Note:** 
> Acquiring the yeast data from NCBI involves use of a 'download tool' known as [the SRA Toolkit](https://www.ncbi.nlm.nih.gov/home/tools/). As the Genomics Analysis module makes use of a virtual machine (VM) running Linux, use of this download tool is covered there.   

## Align Reads

Genome sequencing begins by mapping reads via the `ReadsAligner` command of NGSEP as follows:

<!--- correct paths - account for blob storage & explain mapping reads --->

```bash
java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/ER7A_1.fastq.gz -i2 ../reads/ER7A_2.fastq.gz -s ER7A -o ER7A.bam >& ER7A_aln.log
```

<!--- log file needed? --->

<!--- could each of the FASTQ files be reads aligned indep? If so, how would the results be combined? --->

NGSEP has been written in the Java programming language and packaged for use as a Java ARchive (JAR) file - a 'zip-inspired' file format for aggregating many files together.  

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

> **Note:**
> NGSEP has been incorporated into the customized software image developed for this module. 

<!--- need to verify --->

The output of NGSEP's `ReadsAligner` will be available via Azure Batch. The binary-format output (i.e., the BAM file) for the ER7A parental strain will be written as output to Azure blob storage. The BAM file has the same reads that were present in the FASTQ input files with one major difference: the reads in the BAM file are aligned with the reference genome (namely _Saccharomyces cerevisiae_).

The sample of interest includes a second strain. Thus, the same NGSEP command needs to be re-run against this strain as follows:

```bash
java -jar ~/academy/bin/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/CBS4C_1.fastq.gz -i2 ../reads/CBS4C_2.fastq.gz -s CBS4C -o CBS4C.bam >& CBS4C_aln.log 
```

The details of the NGSEP options and arguments are analogous to the delineation provided previously. 

<!--- HERE --->

## Sort Mapped Reads 

Use will be made of the BAM file in the Genomics Analysis module. In some case, it will prove convenient to make use of a sorted version of this BAM file. To sort reads for both input strains according to their position in the reference genome, run the following commands via the batch service:

```bash
java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_ER7A I=ER7A.bam O=ER7A_sorted.bam >& ER7A_sort.log
```

and 

```bash
java -jar ~/academy/bin/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_CBS4C I=CBS4C.bam O=CBS4C_sorted.bam >& CBS4C_sort.log.         
```

Here, the mapped reads from NGSEP (namely `ER7A.bam` and `CBS4C.bam`) are sorted by [**Picard**](https://github.com/broadinstitute/picard) - literally a "... set of Java command line tools for manipulating high-throughput sequencing (HTS) data and formats ..." available from [The Broad Institute](https://www.broadinstitute.org/). Note that use is made of a temporary directory for sorting purposes in both cases. For additional details regarding use of Picard, consult the documentation [here](https://broadinstitute.github.io/picard/).

> **Note:**
> Picard has been incorporated into the customized software image developed for this module.

With the reads of the two yeast strains mapped against the reference genome (_Saccharomyces cerevisiae_), the final section of this module places emphasis on statistics. For the purpose of computing statistics, use will be made of the sorted BAM files. Additonally, these same sorted -BAM files will provide the required inputs for the subsequent module on Genomics Analysis. 