# Introduction

By algorithmically exploiting parallelism at the source-code level, GROMACS is “Compute Parallel” (in the lower, right quadrant of the figure below), namely:

- Highly concurrent – meaning computations can be performed simultaneously
- Low-to-moderate granularity – meaning communication and/or synchronization is required periodically 

![Granularity versus Concurrency](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/granularity_vs_concurrency.png "Granularity versus Concurrency")

As Compute Parallel applications take full advantage of scale-up-and-out HPC infrastructures, emphasis is placed on uptake of the capabilities to ensure computations are tractable.  Therefore, the objective of extreme-capability GROMACS simulations is the delivery of simulated trajectories for molecular systems. 

<!--- need to explain scale up/out --->

MPI ?