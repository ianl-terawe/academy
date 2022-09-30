# oneAPI: A Standards-Based Approach for Parallel Programming XPUs

At the present time, and for a variety of reasons, the degree of heterogeneity evident in the processor landscape is concerning. From CPUs to GPUs, IPUs to TPUs, along with FPGAs, emerging and next-generation HPC architectures convey heterogeneity as the norm. As the burden of frequently refactoring and reimplementing at the source-code level is prohibitive, a solution for the software part of the HPC solution stack is required. 

oneAPI has emerged to address the challenge of heterogeneous XPUs (see figure below). Championed by Intel and numerous others, oneAPI seeks to promote uptake of Data Parallel C++ (DPC++) – a standards-based implementation of the C++ language with support for programmatically exploiting parallelism. With code written in DPC++ then, support for heterogeneous processors (aka. XPUs) is handled by the toolchain – and offloaded completely from the developer. Not surprisingly, the GROMACS community has become early adopters of oneAPI; in fact, only a single flag needs to be added (-DGMX_GPU=SYCL) to make use of the Intel oneAPI toolchain (i.e., Intel oneAPI DPC++). 

![oneAPI solution stack](/hpc/prototyping/media/oneAPIstack.png "oneAPI solution stack")


Of course, what applies to GROMACS can apply to any application: by adopting oneAPI, the entire XPU landscape presents as opportunities for uptake, as opposed to barriers to progress. To ensure the adoption barrier for oneAPI is as low as it can be, various tooling is available. For example, conversion utilities can be employed to convert proprietary code written in CUDA for NVIDIA GPUs to DPC++ for any processor.  Importantly, post conversion, it has also been demonstrated that applications built with oneAPI perform as well as processor-specific implementations – typically to with a few percentage points. Again, given the upside of XPU neutrality, minor sacrifices in performance seem well justified.
