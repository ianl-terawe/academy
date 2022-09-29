# Reusable Batch-Based Pipelines 

Azure Batch allows for implementation of a simple genomics pipeline. As multiple samples _typically_ require processing, the question that springs to the mind of the genomics researcher is:

> can batch-based pipelines be reused? 

The case of multiple, unknown yeast samples can be drawn upon again for the purpose of answering this important question. 

## Multiple Samples 

ER7A was _one of two_ parental yeast strains requiring attention. In Module 1, the _same_ **five steps** were painstakingly _repeated_ for the CBS4C strain, namely:

1. `java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/CBS4C_1.fastq.gz -i2 ../reads/CBS4C_2.fastq.gz -s CBS4C -o CBS4C.bam >& CBS4C_aln.log`
1. `java -jar ~/javaPrograms/picard.jar SortSam SO=coordinate CREATE_INDEX=true TMP_DIR=tmpdir_sort_CBS4C I=CBS4C.bam O=CBS4C_sorted.bam >& CBS4C_sort.log`
1. `java -jar ~/javaPrograms/NGSEPcore.jar BasePairQualStats -r ../reference/Saccharomyces_cerevisiae.fa -o CBS4C_readpos.stats CBS4C_sorted.bam`
1. `java -jar ~/javaPrograms/NGSEPcore.jar CoverageStats -i CBS4C_sorted.bam -o CBS4C_coverage.stats`
1. `java -jar ~/javaPrograms/picard.jar CollectInsertSizeMetrics I=CBS4C_sorted.bam O=CBS4C_insertLength.stats H=CBS4C_insertLength.pdf`

Obviously, the same procedure 