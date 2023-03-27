# Workspace Introduction 

Open the Workspace for this module. This Workspace provides a _simplified_ interface for Azure Batch - a workload manager that allows you to submit jobs and tasks.

Using the interface, create a new job. Then, create a new task by pasting the following 

```bash
/bin/sh -c ". /opt/intel/oneapi/setvars.sh && . /usr/local/gromacs/bin/GMXRC && gmx --version"
```

into the "command line" field. The details of this 'command' are as follows:

- `/bin/sh -c` invokes the Bourne shell for execution of the commands enclosed within the double quotes
- The Intel oneAPI toolchain and GROMACS are configured for use by 'sourcing' their configuration files 
- `gmx --version` provides version information and a whole lot more (as illustrated below)

Click on `Submit`. 

The purpose of this simple task is to _ensure_ GROMACS is running correctly via Azure Batch. 

Once complete, you should output similar to that shared in the previous section. 

<!--- ![NGSEP commands partial list](/genomics/sequencing/media/ngsep_commands_partial.png "NGSEP commands partial list") 

This image captures only a _partial_ list of NGSEP's modules; included is a brief description for each. 

The full list of NGSEP commands will be available as the output of the task run by Azure Batch. Once your task is complete, view the output by clicking on "View Output". 

--->

<!--- fix the above once UI is known --->

GROMACS was executed on a compute node of the Azure Batch service. The compute node makes use of a customized software image. In addition to the operating system (Linux CentOS 7.9), this software image includes the Intel oneAPI toolchain along with GROMACS. 

<!--- add arch schematic of Batch service implementation --->

You've confirmed you can run workloads via Azure Batch. In the next section, you'll run other jobs. 