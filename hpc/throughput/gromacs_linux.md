# GROMACS on Azure-Based Linux VMs

The position of those responible for leading GROMACS development has always been that the application should execute on platforms spanning from isolated laptops and desktops to the largest supercomputers on the planet. For this module, GROMACS has been built on Azure by making use of the platform illustrated below. From the top down, the main components of this platform are as follows:

- The application - in this case, GROMACS 
- HPC middleware - in general, and optional, a workload manager
- HPC toolchain - in this case, the Intel oneAPI toolchain 
- HPC compute nodes - in this case, a D-Series Intel based VM are used, though numerous VM possibilities exist 

Because ManageX delivers managed services for the entire platform, it has been represented visually as spanning the full-depth of the stack in this representation. 

![GROMACS via oneAPI on Azure](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/GMX_oneAPI_Azure.png "GROMACS via oneAPI on Azure")

> **Note:** 
> D-Series VMs are the emphasis here for learning purposes. GROMACS for throughput would benefit from many-core VMs (e.g., H Series) in production deployments, however. 

In Module 1, an isolated VM was featured. As a self-contained environment for prototyping HPC applications on Windows, this VM _did not_ make use of a workload manager. In this and the subsequent module, however, Azure Batch is introduced as the workload manager. Additionally, use will be made of the Linux operating environment in these latter modules. 

Briefly, the GROMACS application was built from the Linux command line using the following syntax:

```bash
cmake ../. -DCMAKE_C_COMPILER=icx -DCMAKE_CXX_COMPILER=icpx -DGMX_FFT_LIBRARY=mkl -DREGRESSIONTEST_DOWNLOAD=ON
```

Notable with respect to this invocation are each of the following:

- Use of [cmake](https://cmake.org/) - a generic utility that aids in specifying configurations for the GROMACS build process  
- Use of the Intel oneAPI compilers - in this case, specifically the C and C++ compilers as GROMACS is written natively in these languages 
- Use of Intel oneAPI libraries - in this case, the Fast Fourier Transform (FFT) from the Math Kernel Library 
- The availability of regression tests 

Detailed instructions for building GROMACS can be found [here](https://manual.gromacs.org/current/install-guide/index.html). 

> **Note:** 
> As documented [here](https://www.intel.com/content/www/us/en/develop/documentation/get-started-with-intel-oneapi-base-linux/top/before-you-begin.html), the Intel oneAPI toolchain is dependent upon the GNU build toolchain to provide a complete C/C++ development environment in the Linux case. 

To make use of GROMACS, the environment needs to be set up as follows:

```bash
source /usr/local/gromacs/bin/GMXRC 
```

Details of the installed version of GROMACS can then be obtained by issuing the command `gmx --version`. From the output captured in the figure below it is evident that highlights include:

- Shared (OpenMP) and distributed-memory (MPI) parallelism being enabled 
- The Intel® Advanced Vector Extensions 512 (Intel® AVX-512) instructions being employed to enhance performance
- Use of the Fast Fourier Transform (FFT) from the Intel Math Kernel Library 

![Details of the GROMACS implementation](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/gmx_version.png "Details of the GROMACS implementation")

`make check` initiates the correctness of the GROMACS build. After running almost 90 tests, the outcome is summarized as in the figure below.

![GROMACS regression tests - summary](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/gmx_regression_tests.png "GROMACS regression tests - summary")

As the tests were passed, installation of the software can proceed. The built, tested, and installed version of the GROMACS software is put to use in subsequent sections of this module. 