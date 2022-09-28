# Some Preliminaries 

From objectives to prerequisites, some preliminaries are the emphasis here. This section concludes with a framing of genomic analysis in terms of a problem statement. 

## Objectives 

Objectives for this module fall into three categories.

### Knowledge 

Upon completion of this module, the student will know:

- How genomic analysis can be achieved via various computational tasks 
- How genetic sequences of unknown origin can be characterized relative to some reference genome to draw out variations and genotypes for the unknown population 
- How cloud-based infrastructures are ideally suited computational platforms for genomics workloads
- How genomic analysis establishes a foundaton for subsequent analyses 

### Skills 

Upon completion of this module, the student will be able to:

- Analyze sequenced genetic data through use of industry-standard software that quantitatively characterizes the unknown 'population'
- Execute data and computationally intensive genomics-analysis tasks via a virtual machine (VM) on Azure 

### Experiential 

Upon completion of this module, the student will have experienced:

- Active learning on Azure - a proactive learning experience that purposely intertwines learning with doing 
- Rapid onboarding onto Azure - an experience that emphasizes ease of use, but primes the student for next steps  

## Prerequisites 

Computational biology is interdisciplinary in nature. Even though this is intended to be an introduction to genomics that places emphasis on analyzing sequenced data, prerequisites span various disciplines and practices:

- Genetics - A high-level, conceptual understanding of molecular genetics is the _minimal_ prerequisite - namely, that the analysis of genetic sequences proceeds by making comparisons between genomes of interest and reference genomes. Moreover, that ultimately an unknown 'population' can be quantitatively characterized (e.g., annotated) by its genotype variations relative to a known reference.
- IT - High-level, conceptual understandings of cloud computing and command-line use of Linux-based VMs comprise the IT-related prerequisites. Although much of the domain-specific software is written in the Java programming language, there is no prerequisite that is placed on the learner. Implicit with the use of a cloud-based VM is the ability to connect via `ssh` through use of a local client. 

<!-- insert ref for ssh clients --->

For those lacking a background in genetics, a variety of resources exist - ranging from high-school level textbooks to online resources of various types that target various levels of learners. Of course, most institutions provide the required background through academic courses. Those well grounded in genetics will be well placed to appreciate this module to a much deeper of detail. 

## Problem Statement 

An unknown species of yeast has been sequenced and data is available in sorted BAM format on the cloud for genetic investigation. (Refer to the first module of this course to better appreciate this starting point.) Thus, the problem can be stated succintly: 

> genetically analyze the unknown yeast species relative to _Saccharomyces cerevisiae_ (a known species for which a reference genome exists).

In terms of specifics, the problem statement can be elaborated to emphasize that:

- Genomic sequence analysis will be employed as the starting point for further analyses 
- The outcomes of the analysis should be a quantified characterization for the unknown 'population' that encapsulates genetic variations in a genomics-appropriate fashion (i.e., makes use of appropriate standards, practices)
- Any outcomes derived here should provide the means to serve as inputs for subsequent analyses 
- Software commonly used by the genomics community should be made throughout 
- Advantage should be taken of the most-appropriate cloud based services 
- Genetics-based outcomes relating to the unknown 'population' are the key measures of success 

> **Note:**
> According to Wikipedia, at least 1,500 species of yeast are known to exist. That being the case, genetic characterization is not a trivial problem. 