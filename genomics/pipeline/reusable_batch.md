# Reusable Pipelines 

Azure Batch allows for implementation of a simple genomics pipeline. As multiple samples _typically_ require processing, the question that springs to the mind of the genomics researcher is:

> can batch-based pipelines be reused? 

The case of multiple, unknown yeast samples can be drawn upon again for the purpose of answering this important question. 

## The Repetitiveness of Multiple Samples 

ER7A was _one of two_ parental yeast strains requiring attention. In Module 1, the _same_ **five steps** were painstakingly _repeated_ for the CBS4C strain, namely:

1. `java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/CBS4C_1.fastq.gz -i2 ../reads/CBS4C_2.fastq.gz -s CBS4C -o CBS4C.bam >& CBS4C_aln.log`
1. `java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_CBS4C I=CBS4C.bam O=CBS4C_sorted.bam >& CBS4C_sort.log`
1. `java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o CBS4C_readpos.stats CBS4C_sorted.bam`
1. `java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i CBS4C_sorted.bam -o CBS4C_coverage.stats`
1. `java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=CBS4C_sorted.bam O=CBS4C_insertLength.stats H=CBS4C_insertLength.pdf`

Obviously, the procedure detailed in the previous section _can_ be repeated: using the Workspace for this module, make use of the interface to Azure Batch to create all-five tasks with the appropriate dependencies for the CBS4C parental strain. This will this work. There is merit from both user productivity and scientific perspectives. 

However, as far as the tasks ultimately submitted to Azure Batch are concerned, all that has changed is that `ER7A` has been replaced by `CBS4C`. In other words, the name of one unknown sample has been replaced by another. If there are more than two samples to process, the 'value proposition' for further degrees of automation becomes increasingly pressing. 

## Accounting for Multiple Samples

A starting point for automating the multiple-sample scenario rests in the observation that:

> all that has changed is that `ER7A` has been replaced by `CBS4C`.

Thus, treating the name of the yeast strain as a **variable** would allow for a _single_ articulation of the pipeline to be reused. To make this concrete, consider genericized version of the above five steps:

1. `java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/$YSTRAIN_1.fastq.gz -i2 ../reads/$YSTRAIN_2.fastq.gz -s $YSTRAIN -o $YSTRAIN.bam >& $YSTRAIN_aln.log`
1. `java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_$YSTRAIN I=$YSTRAIN.bam O=$YSTRAIN_sorted.bam >& $YSTRAIN_sort.log`
1. `java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o $YSTRAIN_readpos.stats $YSTRAIN_sorted.bam`
1. `java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i $YSTRAIN_sorted.bam -o $YSTRAIN_coverage.stats`
1. `java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=$YSTRAIN_sorted.bam O=$YSTRAIN_insertLength.stats H=$YSTRAIN_insertLength.pdf`

Note that `CBS4C` has been replaced by the variable `$YSTRAIN` - literally a placeholder for the strain of the yeast sample. If the `$YSTRAIN` variable can be cycled through each of the two strains (i.e., `ER7A` and `CBS4C`) then, a reusable pipeline is achievable in principle. To make this clearer, consider the following **pseudocode** implementation:

```bash
foreach (ER7A CBS4C) {
    `java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/$YSTRAIN_1.fastq.gz -i2 ../reads/$YSTRAIN_2.fastq.gz -s $YSTRAIN -o $YSTRAIN.bam >& $YSTRAIN_aln.log`
    `java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_$YSTRAIN I=$YSTRAIN.bam O=$YSTRAIN_sorted.bam >& $YSTRAIN_sort.log`
    `java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o $YSTRAIN_readpos.stats $YSTRAIN_sorted.bam`
    `java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i $YSTRAIN_sorted.bam -o $YSTRAIN_coverage.stats`
    `java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=$YSTRAIN_sorted.bam O=$YSTRAIN_insertLength.stats H=$YSTRAIN_insertLength.pdf`
}
```

> **Note:**
> Pseudocode is _not_ intended to be executed via the Workspace or otherwise. It is employed here for the purpose of illustrating the transition to a reusable pipeline. 

Thus, the pipeline pseudocode is repeated for each of the two samples. Of course, this ignores the dependencies known to be present in the analysis.

## Accounting for Multiple Samples with Dependencies 

Pipeline pseudocode that _includes_ task dependencies might be introduced as follows:

```bash
foreach (ER7A CBS4C) {

# Align reads 

    $TASKLABEL=$YSTRAIN+$READSALIGNER

    `java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/$YSTRAIN_1.fastq.gz -i2 ../reads/$YSTRAIN_2.fastq.gz -s $YSTRAIN -o $YSTRAIN.bam >& $YSTRAIN_aln.log` 

# Sort aligned reads

    if ( EXITSTATUS($TASKLABEL)=0 ) then {

        $TASKLABEL=$YSTRAIN+$SORTREADS

        `java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_$YSTRAIN I=$YSTRAIN.bam O=$YSTRAIN_sorted.bam >& $YSTRAIN_sort.log` 

# Compute stats

        if ( EXITSTATUS($TASKLABEL)=0 ) then {

            `java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o $YSTRAIN_readpos.stats $YSTRAIN_sorted.bam`
            `java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i $YSTRAIN_sorted.bam -o $YSTRAIN_coverage.stats`
            `java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=$YSTRAIN_sorted.bam O=$YSTRAIN_insertLength.stats H=$YSTRAIN_insertLength.pdf`

        }
    }    
}
```

To appreciate the context for this pseudocode consider that:

- Certain steps in the pipeline (e.g., reads alignment and sorting) _require_ labels. Thus, `$TASKLABEL` is dynamically assigned first to the concatenation of the strain and step-unique identifier, namely `$YSTRAIN+$READSALIGNER`. Subsequently, the label is assigned to `$YSTRAIN+$SORTREADS`. 
- Conditional statements determine whether the next step(s) is/are executed. Using the `EXITSTATUS` function, the status of the step identified by `$TASKLABEL` is tested. If, and only if, the step completed successfully is the pseudocode inside the conditional block excuted. Starting from the top, reads are only sorted by Picard if they were successfully aligned by NGSEP's `ReadsAligner`. Subsequently, statistics are only computed if reads were successfully sorted by Picard. 
- Pseudocode within a conditional block is executed sequentially. Thus, each of the three statistical calculations is executed in sequence. 

> **Note:**
> Pseudocode is _not_ intended to be executed via the Workspace or otherwise. It is employed here for the purpose of illustrating the transition to a reusable pipeline. 

Notably absent from this pseudocode is means for interacting with the batch system. This is considered next. 

## Reusable Batch Based Pipelines

Up to this point, use has been made of a Workspace that provides a customized GUI for Azure Batch that supports task dependencies. Implementation of a reusable pipeline, as detailed via the pseudocode above for example, would necessitate additional customization of this GUI. 

Alternatively, command-line and programmatic interfaces for Azure Batch exist. Any of these interfaces would permit implementation of a reusable pipeline based on the pseudocode provided above. 

Even though implmentation and use of a reusable pipeline are beyond the current scope, the feasibility of the same is clear. Subsequent sections delve into the details of reusable pipelines for genomics in greater detail. 

## Additional Considerations 

Motivated by Module 1, a simple example has been employed for the purpose of illustrating reusable pipelines. Obviously, limitations exist. For example, parental strains of the unknown yeast sample were split across two files. As this won't always be the case, the 'genericization process' will need to account for this variability. 

The pipeline considered was comprised of five steps. Clearly, this won't address all needs. 

The nature of genomics is such that such nuances need to be accounted for. Not surprisingly then, support for genomics pipelines is a subject unto itself; an introduction is provided in a subsequent section. 

From this section, however, the following emerge as the high-level requirements for genomics pipelines:

- A means for **describing** the entire pipeline must exist. Any 'pipeline language' must permit articulation of tasks, account for their requirements (e.g., input and output data, minimum numbers of vCPUs, amount of RAM), dependencies, etc. Being able to account for the repetitiveness of similar tasks is desirable, if not essential.
- A means for **executing** tasks. 

<!--- could elaborate --->