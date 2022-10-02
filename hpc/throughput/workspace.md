# Workspace Introduction 

Open the Workspace for this module. This Workspace provides a _simplified_ interface for Azure Batch - a workload manager that allows you to submit jobs and tasks.

Using the interface, create a new job. Then, create a new task by pasting the following 

```shell
gmx ...
```

into the "command line" field. Click on `Submit`. 

The purpose of this simple task is to _ensure_ GROMACS is running correctly via Azure Batch. 

Once complete, you should output similar to:

<!--- ![NGSEP commands partial list](/genomics/sequencing/media/ngsep_commands_partial.png "NGSEP commands partial list") 

This image captures only a _partial_ list of NGSEP's modules; included is a brief description for each. 

The full list of NGSEP commands will be available as the output of the task run by Azure Batch. Once your task is complete, view the output by clicking on "View Output". 

--->

<!--- fix the above once UI is known --->

GROMACS was executed on a compute node of the Azure Batch service. The compute node makes use of a customized software image. In addition to the operating system (Linux Ubuntu 18.04), this software image includes a version of the Java runtime environment along with NGSEP. 

<!--- add arch schematic of Batch service implementation --->

> **Note:** 
> The throughput-based HPC module makes use of a virtual machine (VM) running Linux. You'll be able to make use of this VM to reveal more about this custom software image.

You've confirmed you can run workloads via Azure Batch. In the next section, you'll run other jobs. 


![GROMACS via oneAPI on Azure](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/throughput/media/GMX_oneAPI_Azure.png "GROMACS via oneAPI on Azure")