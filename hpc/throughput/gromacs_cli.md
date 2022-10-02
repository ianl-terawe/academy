# ???

The position of those responible for leading GROMACS development has always been that the application should execute on platforms spanning from isolated laptops and desktops to the largest supercomputers on the planet. GROMACS has been built on Azure by making use of the platform illustrated below. From the top down, the main components of this platform are as follows:

- The application - in this case, GROMACS 
- HPC middleware - in general, and optional, workload managers 
- HPC toolchain - in this case, the Intel oneAPI toolchain 
- HPC compute nodes - various possibilities exist, from isolated VMs with minimal capabilities to many-core VMs interconnected with a low-latency, high-bandwidth fabric 

Because ManageX delivers managed services for the entire platform, it has been represented visually as spanning the full-depth of the stack in this representation. 

![GROMACS via oneAPI on Azure](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/GMX_oneAPI_Azure.png "GROMACS via oneAPI on Azure")

In Module 1, an isolated VM was featured. As a self-contained environment for prototyping HPC applications, this VM did not make use of a workload manager. In this and the subsequent module, a workload manager is introduced. Additionally, use will be made of the Linux operating environment in these latter modules. 

Briefly, the GROMACS application was build from the Linux command line using the following syntax:

```bash
cmake ../. -DCMAKE_C_COMPILER=icx -DCMAKE_CXX_COMPILER=icpx -DGMX_FFT_LIBRARY=mkl -DREGRESSIONTEST_DOWNLOAD=ON
```

Notable with respect to this invocation are each of the following:

- Use of cmake - a generic utility to aid in the build process for applications such as GROMACS 
- Use of the Intel oneAPI compilers - in this case, specifically the C and C++ as GROMACS is written in these languages 
- Use of Intel oneAPI libraries - in this case, the Fast Fourier Transform (FFT) from the Math Kernel Library 
- The availability of regression tests 

Detailed instructions for building GROMACS can be found [here](https://manual.gromacs.org/current/install-guide/index.html). 




