# Computing Statistics 

Use can be made of NGSEP to quantify mapped reads via statistical measures. 

According to the [NGSEP Tutorial](https://sourceforge.net/projects/ngsep/files/training/Tutorial.txt/download), there are three measures that prove to be the most useful. 

## Quality Statistics 

To assess the sequencing quality of each position of the reads, the following commands need to be submitted for execution via the batch system:

```bash
java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o ER7A_readpos.stats ER7A_sorted.bam
```

and 

```bash
java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o CBS4C_readpos.stats CBS4C_sorted.bam
```

In each case, the `BasePairQualStats` command of NGSEP computes these statistics relative to the reference genome (*Saccharomyces_cerevisiae*); documentation for this command is available [here](https://sourceforge.net/projects/ngsep/files/Library/). 

## Coverage Statistics 

For the average coverage of each nucleotide in the genome, the following commands need to be submitted for execution via the batch system:

```bash
java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i ER7A_sorted.bam -o ER7A_coverage.stats
```

and 

```bash
java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i CBS4C_sorted.bam -o CBS4C_coverage.stats
```

In each case, the `CoverageStats` command of NGSEP computes these statistics; documentation for this command is available [here](https://sourceforge.net/projects/ngsep/files/Library/). 

## Size Statistics 

Finally, for the average fragment length, the following commands need to be submitted for execution via the batch system:
       
```bash
java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=ER7A_sorted.bam O=ER7A_insertLength.stats H=ER7A_insertLength.pdf
```

and 

```bash
java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=CBS4C_sorted.bam O=CBS4C_insertLength.stats H=CBS4C_insertLength.pdf
```

Here, use is made of **Picard** to compute fragment-length statistics; documentation for this software can be found [here](https://broadinstitute.github.io/picard/). In turn, Picard depends on **R** - literally "... a free software environment for statistical computing and graphics" available [here](https://www.r-project.org/). Whereas the `.stats` files are ASCII format, the PDF file contains graphical output. 

> **Note:**
> Both Picard and R have been incorporated into the customized software image developed for this module.

## Statistical Roundup 

In addition to the results of the reads-mapping process, various statistical measures are now available - i.e., as ASCII-format `.stats` files. 

> **Note:** 
> Use is made of the *sorted* BAM files for each of the yeast strains in the computation of each of the above statistical measures. 