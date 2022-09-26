This how you sequence the yeast data:

```bash
java -jar ~/javaPrograms/NGSEPcore.jar ReadsAligner -r ../reference/Saccharomyces_cerevisiae.fa -i ../reads/ER7A_1.fastq.gz -i2 ../reads/ER7A_2.fastq.gz -s ER7A -o ER7A.bam >& ER7A_aln.log
```

