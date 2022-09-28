# Variants discovery and genotyping over multiple samples

Assuming your [Workspace is ready for use](/genomics/analysis/workspace.md), type the `MultisampleVariantsDetector` command of NGSEP at the Linux shell prompt as follows:

```bash
$ java -jar ~/javaPrograms/NGSEPcore.jar MultisampleVariantsDetector -maxBaseQS 30 -maxAlnsPerStartPos 2 -knownSTRs ../reference/Saccharomyces_cerevisiae_STRs.txt -r ../reference/Saccharomyces_cerevisiae.fa -o yeastDemo.vcf CBS4C_sorted.bam ER7A_sorted.bam >& yeastDemoMVD.log
```

Recall that NGSEP has been written in the Java programming language and packaged for use as a Java ARchive (JAR) file - a 'zip-inspired' file format for aggregating many files together.  

The options and arguments of NGSEP's `MultisampleVariantsDetector` command are as follows: 

- `maxBaseQS` - establishes the maximum value allowed for a base quality score, and set here to the default value of `30`
- `maxAlnsPerStartPos` - establishes the maximum number of alignments allowed to start at the same reference site, and set here to the default value of `5`
- `knownSTRs` - identifies the file (`Saccharomyces_cerevisiae_STRs.txt`) with known Short Tandem Repeats (STRs)
- The reference genome - indicated by the `-r` flag, this reference is _Saccharomyces cerevisiae_ detailed in FASTA format
- Inputs of interest - split across two sorted BAM format files, the CBS4C and ER7A parental strains are provided as input from local storage 
- Output - indicated by the `-o` flag, `yeastDemo.vcf` is the name of the Variant Call Format (VCF) file that comprises the output 
- Redirected standard output - redirected as indicated above, standard output and standard error are stored in a log file 

> **Note:**
> The file `Saccharomyces_cerevisiae_STRs.txt` can be derived from the reference genome data via an `awk` incantation. 

Briefly, executon of this command results in a database of variants. Included in the VCF file is genotype information relating to the samples of interest. It is noteworthy that indels and STRs that are variable within the samples are included in the analysis.