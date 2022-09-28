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

- Featuring more unknown sample 
- Addressing more complex organisms 
- Involving additional processing steps 

