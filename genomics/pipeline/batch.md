# Batch-Based Pipelines 

## Azure Batch Revisited 

By making use of Azure Batch, the implementation of a _simple_ genomics pipeline can be illustrated. To ensure the example is as relevant and useful as possible, steps from Module 1 will be recontextualized here. 

The Module 1 steps can be summaraized as follows:

- Align reads
- Sort aligned reads 
- Compute statistics 

In Module 1, each of these steps was executed independently and in order - i.e., each step was executed as a separate task by Azure Batch. That 'in order' statement is critical one; clearly, statistics cannot be computed if a genome has not been reads aligned. Stated differently, the ability to quantify the genome statistically is _dependent_ upon having reads-aligned data. (Even better if it's sorted data that has been reads aligned.) 

Thus, the logical question that emerges is: 

> does Azure Batch have support for dependent tasks? 

Given the title of the next section, it's clear the answer to this question is Yes. That being the case, our efforts can continue. 

## Dependent Tasks 

Azure Batch abstracts the management of workload via jobs and tasks. In Module 1, there was a 1-1 relationship between jobs and tasks - i.e., every job had a _single_ task. To make the notion of a pipeline more concrete, here a job will have _multiple_ tasks. To make this example even more concrete, consider the need to sequence the ER7A parental strain of the unknown yeast sample. Let's associated job ID 1 from the batch service with this sequencing requirement. Using this single job identifier, three tasks can be created to account for the required steps - namely a step each for reads aligning, sorting the reads-aligned result, and computing one of the statistical measures. 

Using your Workspace for this module, enter tasks for each of the three steps via the GUI; for example:

1. `java -jar /opt/NGSEP/NGSEPcore.jar ReadsAligner -r /mnt/genomics/reference/Saccharomyces_cerevisiae.fa -i /mnt/genomics/reads/ER7A_1.fastq.gz -i2 /mnt/genomics/reads/ER7A_2.fastq.gz -s ER7A -o /mnt/output/<USERNAME>/ER7A.bam >& /mnt/output/<USERNAME>/ER7A_aln.log`
1. `java -jar /opt/picard/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=/mnt/output/<USERNAME> I=/mnt/output/<USERNAME>/ER7A.bam O=/mnt/output/<USERNAME>/ER7A_sorted.bam >& /mnt/output/<USERNAME>/ER7A_sort.log`
1. `java -jar /opt/NGSEP/NGSEPcore.jar BasePairQualStats -r /mnt/genomics/reference/Saccharomyces_cerevisiae.fa -o /mnt/output/<USERNAME>/ER7A_readpos.stats /mnt/output/<USERNAME>/ER7A_sorted.bam`

Using the interface for Azure Batch in the Workspace, ensure you indicate the need to make use of support for **dependent tasks** as well the specifics of the dependency. The screenshot below makes the dependent-task requirement clear. 

![Azure Batch - dependent tasks](https://raw.githubusercontent.com/ianl-terawe/academy/main/genomics/pipeline/media/dependent_task.png "Azure Batch - dependent tasks")

Execute these tasks via your Workspace. Note that the sorting of the BAM via Picard doesn't begin until NGSEP has completed its reads alignment. Similarly, the computation of the quality statistics via NGSEP will not begin until after Picard has completed sorting the BAM file. 

It's important to note that, by making use of task dependencies in Azure Batch, a simple **genomics pipeline** has been implemented. 

The quality of the reads-aligned data was the first of three statistical measures. In the following section, emphasis is placed on all-three measures. 

<!--- screenshot req'd task status? --->

## Parallelized Dependent Tasks 

Statistics quantifying the quality of the reads-alignment process were one of three statistical measures obtained in the first module of this course. An additional two measures are needed. The input required for _all three_ of these statistical measures is the _same_, namely the sorted BAM file that results from use of Picard. Once the sorted BAM is available then, the computation of _all-three_ statistical measures can proceed _in parallel_.

Using your Workspace for this module, _re-enter_ the first, two tasks via the GUI as you did above; namely: 

1. `java -jar /opt/NGSEP/NGSEPcore.jar ReadsAligner -r /mnt/genomics/reference/Saccharomyces_cerevisiae.fa -i /mnt/genomics/reads/ER7A_1.fastq.gz -i2 /mnt/genomics/reads/ER7A_2.fastq.gz -s ER7A -o /mnt/output/<USERNAME>/ER7A.bam >& /mnt/output/<USERNAME>/ER7A_aln.log`
1. `java -jar /opt/picard/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=/mnt/output/<USERNAME> I=/mnt/output/<USERNAME>/ER7A.bam O=/mnt/output/<USERNAME>/ER7A_sorted.bam >& /mnt/output/<USERNAME>/ER7A_sort.log`

Note the task ID corresponding to sorting via Picard (the second task above); make each of the following three statistical computations dependent upon this sorting task:

1. `java -jar /opt/NGSEP/NGSEPcore.jar BasePairQualStats -r /mnt/genomics/reference/Saccharomyces_cerevisiae.fa -o /mnt/output/<USERNAME>/ER7A_readpos.stats /mnt/output/<USERNAME>/ER7A_sorted.bam`
1. `java -jar /opt/NGSEP/NGSEPcore.jar CoverageStats -i /mnt/genomics/ER7A_sorted.bam -o /mnt/output/<USERNAME>/ER7A_coverage.stats`
1. `java -jar /opt/picard/picard.jar CollectInsertSizeMetrics I=/mnt/output/<USERNAME>/ER7A_sorted.bam O=/mnt/output/<USERNAME>/ER7A_insertLength.stats H=/mnt/output/<USERNAME>/ER7A_insertLength.pdf`

Execute these tasks via your Workspace and make note of the task status. Note that computation of the various statistics will not begin until after Picard has completed sorting the BAM file. For various reasons, these statistical results may take different amounts of time to appear. Because they are only dependent upon the sorted BAM file, and completely independent of each other, that's completely fine. 

> **Note:**
> From quality to coverage to size metrics, the statistical measures may present with widely varying computational demands. Additionally, as the size-metrics example illustrates, there may be data-intensive requirements - e.g., the conversion of output into a graphical format rendered via a PDF file. Finally, Azure Batch makes use of algorithms to schedule workload for processing; these algorithms take into consideration the taks identified here alongside requests from other users. Collectively then, there exist a number of reasons why results will appear at different times. In fact, if the same pipeline is re-executed, results may appear in a different order; this is to be expected. 

Thus, a pipeline with varying dependencies can be constructed and executed via Azure Batch. Because the batch service now executes workload _without_ the need for intervention, the **automation** achieved through this pipeline results in the user being 'freed up' to work on other tasks - e.g., other samples (see next section). Recall that reads alignment via NGSEP took of order 30-60 minutes. In Module 1, you likely checked multiple times for completion of this computationally intensive task. Thus, the value of an automated pipeline is _significantly amplified_ when each of the tasks take different amounts of time - especially if one or more tasks takes a significant amount time. In addition to benefits cited elsewhere in this module (e.g., scientific repeatability and reproducibility), making genomics researchers more productive needs to be added to this list. 

<!--- 
## Failure Modes 

To be added ... 

---> 

<!--- workflow vs. pipeline  --->