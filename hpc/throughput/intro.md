# Introduction

## GROMACS as an HPC Throughput Application

To illustrate HPC that aims to maximize the throughput of computational workloads use is made of the GROMACS application. This places GROMACS on the right side of the figure below. Thus, multiple runs of moderate-capability simulations are the objective. Each simulation is crafted to ‘fit’ within the confines of, for example, a many-core virtual machine (VM).

![Granularity versus Concurrency](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/granularity_vs_concurrency.png "Granularity versus Concurrency")

> **Note:**
> Traditionally, GROMACS has been exploited as a capability-oriented HPC application. In Module 3, GROMACS is revisited from this traditional perspective - namely that of single-run extreme capability simulations. 

As only a single VM is used for 'scale-up' purposes, other VMs can run simulations based on _different_ input parameters. The objective of GROMACS use cases framed in this fashion is that of **throughput**. In other words, by maximizing the number of simulations performed per unit wall-clock time, an **ensemble** of runs is employed to investigate use cases of interest. As the figures below well illustrates, ensembles of runs can take a variety of forms.

![Ensembles of runs](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/ensemble.png "Ensembles of runs")

This is an interesting and significant departure for GROMACS, as maximizing for throughput is typically the domain of applications that can exploit parallelism inherent in data (upper, right quadrant of the granularity versus concurrency figure above).

For example, genomic sequence analysis is typical of the “Data Parallel” case. Using applications such as BLAST, for example, the resulting embarrassingly parallel workload is a matrix of computations comprised of ‘chunks’ of data destined for execution on a single processing core. Thus, the case here with GROMACS is distinctive in that it features the throughput aspects of the “Data Parallel” case combined with a reasonable degree of capability.

Throughput-oriented GROMACS molecular dynamics simulations do, however, have an important characteristic in common with their Data Parallel counterparts: because each run is independent, there is absolutely no requirement for a low-latency, high-bandwidth interconnect fabric. While it is possible that post-computation results from an ensemble of runs may need to be aggregated in some sense, there is absolutely no requirement for ‘ongoing communication’ _during_ execution. This non-trivial distinction serves to underscore the following point: maximizing for throughput is a _fundamentally different objective_ than is maximizing for extreme capability. 
