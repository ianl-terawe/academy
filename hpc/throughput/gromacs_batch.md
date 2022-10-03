# GROMACS Throughput Workloads 

## Running GROMACS Throughput Workloads via Azure Batch 

GROMACS has been introduced in previous sections. The emphasis here is running a typical GROMACS workload via Azure Batch. 

Representative benchmarks are available from the Max Planck Institute for Multidisciplinary Sciences [here](https://www.mpinat.mpg.de/grubmueller/bench). From this site, two, standard benchmarks have been retrieved as follows:

- MEM - comprising 82,000 atoms and requiring a 2 femtosecond timestep, MEM is a protein in a membrane surrounded by water 
- RIB - comprising 2,000,000 atoms and requiring a 4 femtosecond timestep, RIB is a ribosome in water 

The details of each is captured via a `tpr` file - a binary-format and portable file that captures the system topology, parameters, coordinates, and velocities (according to [the documentation](https://manual.gromacs.org/current/reference-manual/file-formats.html#tpr)). Using each of the `tpr` files as input various benchmarks can be run. 

For example, tuning runs can be executed by entering the following as the "command line" panel of the interface to Azure Batch in this module's Workspace:

```bash
gmx mdrun -s <PATH_TO_TPR_FILES>/benchMEM.tpr -nsteps 10000 -resethway -cpt 1440   
```

Although [the documentation](https://manual.gromacs.org/current/onlinehelp/gmx-mdrun.html) should be consulted for the details, the idea here is as follows:

- Executes `mdrun` - namely, the main computational chemistry engine within GROMACS
- Make use of the `MEM tpr` file as input 
- Run GROMACS for 10,000 steps 
- Reset the load balancing at the half-way point 
- Checkpoint the intermediate results of the simulation every 1440 mins (or 24 hours) 

Expected output will end as follows:

![GROMACS tuning example with a protein in a membrane surrounded by water](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/gmx_tuning_mem.png "GROMACS tuning example with a protein in a membrane surrounded by water")

Similar results can be obtained for RIB:

```bash
gmx mdrun -s <PATH_TO_TPR_FILES>/benchRIB.tpr -nsteps 10000 -resethway -cpt 1440   
```

![GROMACS tuning example with a ribosome in water](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/gmx_tuning_rib.png "GROMACS tuning example with a ribsome in water")

<!--- execution a concern? --->

Not surprisingly, the results of these runs indicate that the molecular dynamics trajectory for the 'membrane system' (namely MEM) is about a factor of 10 longer than are the corresponding results for the more complex 'ribosome system'. Molecular dynamics simulations are so compute intensive that the lifetimes of trajectories are measure in nanoseconds per day (ns/day). 

GROMACS is a complex application comprised of multiple modules. These modules exploit parallelism optimally. The application even has a built-in capability to determine how it can be optimally executed. 

In addition to tuning runs along the lines of the above, benchmarks can also experiment with dynamic load balancing by appending the `-dlb yes` option and value to the `mdrun` command line.  

## GROMACS as a Throughput Application Revisited 

For a given system (e.g., MEM or RIB), framing GROMACS as a throughput application would involve the creation of multiple `tpr` files. Each of these `tpr` files might, for example, systematically vary system topology, parameters, coordinates, and/or velocities. Thus, the outcome of such an ensemble of runs would be characterizing a system of interest across a multidimensional parameter space. 

In stark stark contrast, and in the next module, emphasis is placed on running a given simulation based on a single `tpr` file for a 'long time' - again, where the lifetimes of molecular dynamics simulations are on the order of nanoseconds. 