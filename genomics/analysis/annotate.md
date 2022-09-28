# Annotate 

The Variant Call Format (VCF) file produced in the previous section serves as the starting point here, namely for the purpose of functionally annotating sequenced data. Through annotation, the functional elements along the sequence of a genome are identified. For the first time the process, meaning is introduced for each variant in the yeast samples of interest. 

NGSEP's `VCFAnnotate` command needs to be run at the Linux shell prompt of your Workspace as follows:

```bash
$ java -jar ~/javaPrograms/NGSEPcore.jar VCFAnnotate -i yeastDemo.vcf -t ../reference/Saccharomyces_cerevisiae.gff3 -r ../reference/Saccharomyces_cerevisiae.fa -o yeastDemo_ann.vcf >& yeastDemo_ann.log
```

The details of the options and arguments for NGSEP's `VCFAnnotate` command are as follows:

- Input - indicated as the argument of the `-i` flag, the input is the VCF file `yeastDemo.vcf` produced previously 
- The reference annotations - indicated as the argument of the `-t` flag, annotations of the reference genome are detailed in [General Feature Format (GFF3) format](https://github.com/The-Sequence-Ontology/Specifications/blob/master/gff3.md)
- The reference genome - indicated by the `-r` flag, this reference is _Saccharomyces cerevisiae_ detailed in FASTA format
- Output - indicated as the argument of the `-o` flag, the output `yeastDemo_ann.vcf` is in the VCF file format with annotatiosn included 

> **Note:**
> As the input data for `VCFAnnotate` are already local to your virtual machine (VM), file copying is not required. 

Refer to the [NGSEP reference](https://sourceforge.net/projects/ngsep/files/Library/) for additional details regarding its `VCFAnnotate` command.

As the 'complete database,' the `yeastDemo_ann.vcf` file is a valuable one as it contains all the available information regarding the yeast population of interest; i.e., it contains:

- All the variant positions
- The genotype of each sample at each position
- The functional annotations  of those positions

> **Note:**
> To reiterate, the `yeastDemo_ann.vcf` file is a valuable one. If you were working on a research project, this is a file that you would need to revisit in the future. 

<!--- are there tools to view VCF files? --->

Annotated samples serve as the termination point for this module. Topics such as filtering the annotated VCF file and exporting it to different formats all receive attention in the [NGSEP Tutorial](https://sourceforge.net/projects/ngsep/files/training/Tutorial.txt/download). 