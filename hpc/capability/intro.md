# Introduction

## GROMACS as an HPC Capabilty Application

In the previous module, GROMACS was introduced as an HPC _throughput_ application. Here, GROMACS is considered as an HPC _capability_ application. 

By algorithmically exploiting parallelism at the source-code level, in this case GROMACS is “Compute Parallel” (in the lower, right quadrant of the figure below), namely:

- Highly concurrent – meaning computations can be performed simultaneously
- Low-to-moderate granularity – meaning communication and/or synchronization is required periodically 

![Granularity versus Concurrency](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/granularity_vs_concurrency.png "Granularity versus Concurrency")

Compute Parallel applications take full advantage of their 'scaled-out' HPC infrastructures - i.e., capability HPC is established by making use of many to all compute nodes in an HPC infrastructure. Because the compute nodes are interconnected via a network, the application is necessarily making use of distributed memory in performing computations in parallel. 