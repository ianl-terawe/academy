# Batch 

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

Azure Batch abstracts the management of workload via jobs and tasks. In Module 1, there was a 1-1 relationship between jobs and tasks - i.e., every job had a single task. To make the notion of a pipeline more concrete, here a job will have multiple tasks. To make this example even more concrete, consider the need to sequence the ER7A parental strain of the unknown yeast sample. Let's associated job ID 1 from the batch service with this sequencing requirement. Using this single job identifier, three tasks can be created to account for the required steps - namely a step each for reads aligning, sorting the reads-aligned result, and computing one of the statistical measures. 

Using your Workspace for this module, enter tasks for each of the three steps via the GUI; for example:

1. `java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/ER7A_1.fastq.gz -i2 ../reads/ER7A_2.fastq.gz -s ER7A -o ER7A.bam >& ER7A_aln.log`
1. `java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_ER7A I=ER7A.bam O=ER7A_sorted.bam >& ER7A_sort.log`
1. `java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o CBS4C_readpos.stats CBS4C_sorted.bam`

Using the interface for Azure Batch in the Workspace, ensure you indicate the need to make use of support for dependent tasks as well the specifics of the dependency. The screenshot below makes the dependent-task requirement clear.

<!--- screenshot req'd --->

## Parallelized Dependent Tasks 

stats ... 

<!--- workflow vs. pipeline  --->