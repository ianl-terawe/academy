

sorted BAMs required 



java -jar ~/javaPrograms/NGSEPcore.jar MultisampleVariantsDetector -maxBaseQS 30 -maxAlnsPerStartPos 2 -knownSTRs ../reference/Saccharomyces_cerevisiae_STRs.txt -r ../reference/Saccharomyces_cerevisiae.fa -o yeastDemo.vcf CBS4C_sorted.bam ER7A_sorted.bam >& yeastDemoMVD.log
