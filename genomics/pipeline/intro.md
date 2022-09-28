# Introduction 

<!--- motivation --->

In Module 1, the ER7A parental strain was subjected to:

- Reads alignment 
- Sorting of the aligned reads 
- Statistical characterization of these reads comprising quality, coverage, and size

Implicit in the reads-alignment step was use of _two_ FASTQ format files for the ER7A parental strain; both files were provided as input to the NGSEP `ReadsAligner` command. In other words, the results of sequencing the unknown yeast species needed to be captured across two, ~0.5 GB files. Recall that yeast is an example of a 'small' eukaryote. 

Then, the CBS4C parental strain was subjected to precisely the _same set of steps_. Its sequencing results were also split across two, ~0.5 GB files. 

In Module 2, both parental strains were subjected to futher analyses:

- Variants discovery and genotyping 
- Annotation 
- Filtering 
- Conversion 

> **Note:**
> Filtering and conversion were coverage by reference to the [NGSEP Tutorial](https://sourceforge.net/projects/ngsep/files/training/Tutorial.txt/download). 

As the intention was to work through each step in detail, **automation** was _not_ considered. However, as the summary here illustrates, there are _ample_ opportunities for automation; for example:

- Sequencing (2 tasks) and computing statistics (3 tasks) on a per-sample basis 
- Discovering variants and genotyping on a per-population basis (1 task per population)
- Annotating, filtering, and converting on a per-population basis (3 or more tasks per population)

And this is the case in an example whose primary objective is _just_ learning. In real research projects, prospects are good that the need for automation would be amplified - quite likely, significantly amplified. For example, auotmation might be warranted in cases:

- Featuring more unknown samples - as only two were employed here for the purpose of illustration 
- Addressing more complex organisms - as yeast is a relatively simple organism to characterize genetically 
- Involving additional processing steps - as needs and/or interests dictate

The graphical representation provided below affords the following insights:

- Dependencies exist between some steps - e.g., a genome needs to be reads aligned (and sorted) before its statistics can be computed 
- Some steps can be executed in parallel - e.g., once a genome has been reads aligned, various statistical measures can be independently computed in parallel 
- In some cases, it may prove necesary to carefully repeat the same set of steps in the same order with the same set of parameters - e.g., variants discovery should establish the same maximum allowable value for a base quality score across samples of interest (to avoid this being a source of bias)

Taken collectively, the concerns raised here tease out the fundamental requirements for **genomics pipelines** - i.e., the means for executing a sequence of steps. In this module, emphasis is given to several options for such pipelines that are available on Azure. 

As indicated above, actual research projects need to grapple with increased degrees of complexity. Owing to this complication inherent to genomics, pipelines serve another important purpose: 

> pipelines ensure that results obtained from genomics are repeatable and reproducible. 

<!--- embellish - distinguish --->

By some accounts, repeatability and reproducibilty have reached the epic proportion of a crisis. Thus, pipelines aren't just about automating genomics, they are about ensuring the correct pursuit of the scientific method. 