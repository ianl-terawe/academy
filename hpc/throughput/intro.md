# Introduction

By algorithmically exploiting parallelism at the source-code level, GROMACS is “Compute Parallel” (in the lower, right quadrant of the figure below), namely:

- Highly concurrent – meaning computations are performed simultaneously
- Low-to-moderate granularity – meaning communication and/or synchronization is required periodically 

![Granularity versus Concurrency](/hpc/throughput/media/granularity_vs_concurrency.png "Granularity versus Concurrency")

As Compute Parallel applications take full advantage of scale-up-and-out HPC infrastructures, emphasis is placed on uptake of the capabilities to ensure computations are tractable.  Therefore, the objective of extreme-capability GROMACS simulations is the delivery of simulated trajectories for molecular systems. 

More recently, an interesting trend has emerged in the published literature: single-run extreme capability simulations have been _replaced_ by multiple runs of moderate-capability simulations (the right side of the figure above). To be a little more concrete, in this case, each simulation is crafted to ‘fit’ within the confines of, for example, a many-core VM.


## GROMACS as a Throughput Application

As only a single VM is used for scale-up purposes, other VMs can run simulations based on different input parameters. The objective of GROMACS use cases framed in this fashion is that of throughput. In other words, by maximizing the number of simulations performed per unit wall-clock time, an ensemble of runs is employed to investigate use cases of interest. 

This is an interesting and significant departure for GROMACS, as maximizing for throughput is typically the domain of applications that can exploit parallelism inherent in data (upper, right quadrant of the granularity versus concurrency figure above).

For example, genomic sequence analysis is typical of the “Data Parallel” case. Using applications such as BLAST, for example, the resulting embarrassingly parallel workload is a matrix of computations comprised of ‘chunks’ of data destined for execution on a single processing core. Thus, the case here with GROMACS is distinctive in that it features the throughput aspects of the “Data Parallel” case combined with a reasonable degree of capability.

Throughput-oriented GROMACS MD simulations do, however, have an important characteristic in common with their Data Parallel counterparts: because each run is independent, there is absolutely no requirement for a low-latency, high-bandwidth interconnect fabric. While it is possible that post-computation results from an ensemble of runs may need to be aggregated in some sense, there is absolutely no requirement for ‘ongoing communication’ during execution. This non-trivial distinction serves to underscore the following point: maximizing for throughput is a fundamentally different objective than is maximizing for extreme capability. As scientists and engineers may reasonably seek to have at their disposal this spectrum of options, a third area where challenges emerge is in the infrastructure employed in support of GROMACS use cases

![GROMACS via oneAPI on Azure](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/GMX_oneAPI_Azure.png "GROMACS via oneAPI on Azure")