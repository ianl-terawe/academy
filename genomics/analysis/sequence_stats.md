# Sequence Unknown Samples 

## Install NGSEP 

To sequence the unknow samples against the reference, use is made here of NGSEP. 

From the home directory of your VM (`cd ~`), issue the command:

`mkdir -p ~/academy/bin`

Move into this directory (`cd ~/academy/bin`), and issue the command:

`wget --no-check-certificate https://sourceforge.net/projects/ngsep/files/Library/NGSEPcore_4.2.1.jar`

> **Note:**
> The `--no-check-certificate` option is required to bypass an expired certificate.

To ensure the NGSEP binary is executable, type:

`chmod a+x NGSEPcore_4.2.1.jar`

To save a little bit of typing, it is recommended to make the following symbolic link:

`ln -s NGSEPcore_4.2.1.jar NGSEPcore.jar`

> **Note:**
> In the material that follows, it will be assumed that this link has been made. 

## Align Reads 

Move into the `mapping` directory (`cd ~/academy/ngsep_tutorial/mapping`) and invoke NGSEP's `ReadsAligner` as follows: 

`java -jar ~/academy/bin/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/ER7A_1.fastq.gz -i2 ../reads/ER7A_2.fastq.gz -s ER7A -o ER7A.bam >& ER7A_aln.log`

Refer to Module for a reminder of the details of this command as needed. 

As NGSEP runs locally on your VM, input and output data is handled locally. 

Expect this command to take some 30-60 minutes to complete execution. To monitor progress, you can periodically type:

`tail -20 ER7A_aln.log` 

This will display the last 20 lines of the indicated log file. 

> **Note:**
> The `less` pager offers a more useful way of monitoring the log file as it is being appended in real time.

<!--- video here! --->

To align reads for the other strain of the unknown yeast sample, type:

`java -jar ~/academy/bin/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/CBS4C_1.fastq.gz -i2 ../reads/CBS4C_2.fastq.gz -s CBS4C -o CBS4C.bam >& CBS4C_aln.log`

## Sort Aligned Reads

### Install Picard 

Picard was introduce in Module 1. For present purposes, move over to the `~/academy/bin` directory and then issue the command:

`wget https://github.com/broadinstitute/picard/releases/download/2.27.5/picard.jar`

As above, ensure the JAR file is executable: `chmod a+x picard.jar`

As Picard will create a number of temporary files as it works through the sorting process, it is a recommended practice to issue the command

`mkdir tmpdir_sort_ER7A tmpdir_sort_CBS4C`

for each of the unknown strains.

### Sort with Picard 

Using Picard, sorted `BAM files` can be obtained by issuing the following two commands:

```bash
java -jar ~/academy/bin/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_ER7A I=ER7A.bam O=ER7A_sorted.bam >& ER7A_sort.log
java -jar ~/academy/bin/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_CBS4C I=CBS4C.bam O=CBS4C_sorted.bam >& CBS4C_sort.log 
```

Sorted aligned reads (aka. the sorted `BAM files`) are required for the discovery of variants, genotyping, as well as annotation. This genomic analysis is the subject of subsequent sections. 

## Compute Statistics (Optional)

As was the case in Module 1, for each of the two strains, quality and coverage statistics can be obtained as follows:

```bash
java -jar ~/academy/bin/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o ER7A_readpos.stats ER7A_sorted.bam
java -jar ~/academy/bin/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o CBS4C_readpos.stats CBS4C_sorted.bam

java -jar ~/academy/bin/NGSEPcore.jar CoverageStats -i ER7A_sorted.bam -o ER7A_coverage.stats
java -jar ~/academy/bin/NGSEPcore.jar CoverageStats -i CBS4C_sorted.bam -o CBS4C_coverage.stats
```

As the customized software image used for your VM includes [samtools](http://samtools.sourceforge.net/), an alternative means for acquiring the fragment-length statistics is as follows:

```bash 
samtools view -F 268 ER7A_sorted.bam | awk '{l=$9;if(l>=0){i=sprintf("%d",l/25)+1;if(i<100)a[i]++;else aM++}}END{for(i=1;i<100;i++)print (i-1)*25,a[i];print "More",aM}' > ER7A_insertLength.stats;

samtools view -F 268 CBS4C_sorted.bam | awk '{l=$9;if(l>=0){i=sprintf("%d",l/25)+1;if(i<100)a[i]++;else aM++}}END{for(i=1;i<100;i++)print (i-1)*25,a[i];print "More",aM}' > CBS4C_insertLength.stats;
```

Each of the `.stats` files is ASCII text- as indicated via `file *.stats`.            