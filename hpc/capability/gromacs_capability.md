# GROMACS Capability Workloads 

## Running GROMACS Throughput Workloads via Azure Batch 

In the previous module, the GROMACS application was invoked as follows for throughput-oriented workloads:

```bash
gmx mdrun -s <PATH_TO_TPR_FILES>/benchMEM.tpr -nsteps 10000 -resethway -cpt 1440   
```

For the present case of a capability-oriented workload, the invocation needs to be _prepended_ with `mpirun` as follows:

```bash
mpirun -np 2 gmx_mpi mdrun -s <PATH_TO_TPR_FILES>/benchMEM.tpr -nsteps 10000 -resethway -cpt 1440   
```

Other than making use of `mpirun` across two compute nodes, only `gmx_mpi` is required. Use of `gmx_mpi` ensures that the MPI-enabled version of GROMACS `mdrun` is utilized. 

> **Note:**
> Additional steps are required to build the MPI-enabled version of GROMACS. Refer to the documentation [here](https://manual.gromacs.org/documentation/current/install-guide/index.html#mpi-support).  