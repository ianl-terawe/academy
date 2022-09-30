# Some Preliminaries 

From objectives to prerequisites, some preliminaries are the emphasis here. This section concludes with a framing of genomic pipelines in terms of a problem statement. 

## Objectives 

Objectives for this module fall into three categories.

### Knowledge 

Upon completion of this module, the student will know:

- How genomic pipelines can be employed to automate routine and/or repetitive computational tasks 
- Why genomic pipelines are of significant value to the science as well as the scientist  
- How cloud-based infrastructures are ideally suited computational platforms for genomics pipelines  

### Skills 

Upon completion of this module, the student will be able to:

- Execute a genomics pipeline by making use of Azure Batch 
- Apply the key takeaways from batch-based pipelines to discipline-specific pipelines 

### Experiential 

Upon completion of this module, the student will have experienced:

- Active learning on Azure - a proactive learning experience that purposely intertwines learning with doing 
- Rapid onboarding onto Azure - an experience that emphasizes ease of use, but primes the student for next steps  

## Prerequisites 

Computational biology is interdisciplinary in nature. Even though this is intended to be an introduction to genomics that places emphasis on executing genomics workloads, prerequisites span various disciplines and practices:

- Genetics - A high-level, conceptual understanding of molecular genetics is the _minimal_ prerequisite - namely, that the analysis of genetic sequences proceeds by making comparisons between genomes of interest and reference genomes. Moreover, that ultimately an unknown 'population' can be quantitatively characterized (e.g., annotated) by its genotype variations relative to a known reference.
- IT - High-level, conceptual understandings of cloud computing and workload management comprise the IT-related prerequisites. The notion of making use of a workload-management infrastructure for executing interdependent workflows is desirable. Finally, although much of the domain-specific software is written in the Java programming language, there is no prerequisite that is placed on the learner.  

<!-- insert ref for ssh clients --->

For those lacking a background in genetics, a variety of resources exist - ranging from high-school level textbooks to online resources of various types that target various levels of learners. Of course, most institutions provide the required background through academic courses. Those well grounded in genetics will be well placed to appreciate this module to a much deeper of detail. 

## Problem Statement 

It can take numerous steps to process genetic data - with each step taking similar to very different amounts of time. Typically, the same steps are repeated for each sample of interest. Thus, the problem can be stated succintly: 

> can measures of automation be introduced to reduce the need for researchers to perform routine and/or repetitive tasks in real time? 

In terms of specifics, the problem statement can be elaborated to emphasize that:

- Some processing tasks necessarily depend on others 
- Some processing tasks can be executed in parallel 
- A means for both describing and executing genomics processing pipelines is required 
- Software commonly used by the genomics community should be made throughout 
- Advantage should be taken of the most-appropriate cloud based services 
- Scientific and scientist-specific outcomes are the key measures of success 
