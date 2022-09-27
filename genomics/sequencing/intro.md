# Introduction

The purpose of this module is to sequence genomes. To illustrate this common requirement of genomics, use will be made of yeast samples. These samples will be compared with a reference yeast genome, namely _Saccharomyces cerevisiae_. Known as mapping reads, this aspect of sequence analysis is concluded by the computation of various statistical measures that quantify the comparison. 

Aspects of sequencing are _computationally intensive_; for example, mapping reads is inherently so. As data volumes increase, so does the computational overhead. In addition to making use of software typical to genomics, this module makes use of a batch service on Azure. This allows compute-intensive workloads to be executed _non-interactively_ in a fully-managed fashion. 

The outcome of this module are sorted reads and statistics for the yeast strains of interest. Moreover, this data serves as the primary input for a subsequent module that places the emphasis on analyzed sequenced genomics data. 