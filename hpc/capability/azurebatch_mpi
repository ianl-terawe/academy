# Capability HPC via Azure Batch 

## Azure Batch Configuration Overview

Azure Batch can be used in support of **capability HPC**. Inherent in capability HPC is the distribution of a single application across a network of interconnected compute nodes. At the source-code level, the Message Passing Interface (MPI) is employed to program for distributed-memory parallel computing. MPI-specific code that involves elements of communication and computation is supported by a library. 

To enable Azure Batch for distributed-memory parallel computing (aka. capability HPC), a specific-purpose pool has been added to the ManageX Academy infrastructure. Highlights of this configuration are as follows:

- Compute nodes in the pool are configured to support communication amongst nodes 
- Compute nodes are configured to limit the number of tasks they can execute - a limit typically set to `1`
- Compute nodes make use of a custom software image that includes various libraries - minimally MPI, and likely others to support the needs of the application (e.g., an FFT routine)

## Basic Example 

<!--- need the hello world source code --->

Using the ManageX Academy Workspace for this module, add a new job, and then a new task for Azure Batch. Note that the `MPI` pool needs to be selected. Into the command line field, enter:

```bash
/usr/lib64/openmpi/bin/mpirun -np 2 --host $AZ_BATCH_HOST_LIST -wdir $AZ_BATCH_TASK_SHARED_DIR $AZ_BATCH_TASK_SHARED_DIR/hello-world.exe
```

The highlights of this command-line invocation are as follows:

- The application - the executable, namely `hello-world.exe`, resides in the `$AZ_BATCH_TASK_SHARED_DIR` and appears at the end of the line as the final argument of `mpirun`
- `mpirun` - provided by the MPI library, `mpirun` is the means for invoking the parallelized exection across the identified compute nodes
- `np 2 ` - indicates that `mpirun` is to make use of 2 compute nodes in executing the `hello-world.exe` application 
- `--host $AZ_BATCH_HOST_LIST` - is the dynamically generated list of compute nodes provided by Azure Batch to `mpirun` for executing this workload 
- `-wdir $AZ_BATCH_TASK_SHARED_DIR` - is the storage location where the `hello-world.exe` executable resides

Executing this command via Azure Batch will produce the familiar "Hello, World!" refrain from each of the two nodes involved in the 'computation'. To view this output, click on the task ID in your Azure Batch Workspace; the "Hello, World!" refrain will be displayed at the standard output from executing the `hello-world.exe` application. 

More sophisticated examples are considered in the following section. 