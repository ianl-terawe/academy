# Workspace Introduction 

Your Workspace provides a _simplified_ interface for Azure Batch - a workload manager that allows you to submit jobs and tasks.

Click on `My Workspace`. 

Expand `Workspace Details` by clicking on the downward-pointing arrow or anywhere on this panel.

Locate the `Add` drop down menu and select `Job`. 

For your **New Job**, select the default **Pool**, and enter a **Name** as follows:

!["New Job interface"](/genomics/sequencing/media/new_job.png "New Job interface")

Click submit at the bottom of the `New Job` panel. 

Using the same `Add` drop down menu, select `Task`. 

Create a new task by pasting the following 

```shell
java --version
```

into the `Commands` field. See the screenshot below. 

!["New Task interface"](/genomics/sequencing/media/new_task.png "New Task interface")

Click on `Submit`. 

To view the output generated, select the `Task List` tab, and then the name of your task. 

Once complete, you should see output similar to:

![Task Details](/genomics/sequencing/media/task_details.png "Task Details")

> **Note:**
> Execution of this task may take seconds to minutes. Azure Batch has been configured to dynamically allocate compute nodes to its compute pools based upon queue workload. Thus, in the worst-case scenario (no previously queued or executing workload), Azure Batch will provision and deploy compute nodes 'from scratch.'

<!--- swapped out for Java 

![NGSEP commands partial list](https://raw.githubusercontent.com/ianl-terawe/academy/main/genomics/sequencing/media/ngsep_commands_partial.png "NGSEP commands partial list")

This image captures only a _partial_ list of NGSEP's modules; included is a brief description for each. 

The full list of NGSEP commands will be available as the output of the task run by Azure Batch. Once your task is complete, view the output by clicking on "View Output". 

--->

The command was executed on a compute node of the Azure Batch service. The compute node makes use of a customized software image. In addition to the operating system, this software image includes a version of the Java runtime environment along with NGSEP. 

<!--- add arch schematic of Batch service implementation --->

> **Note:** 
> The Genomics Analysis module makes use of a virtual machine (VM) running Linux. You'll be able to make use of this VM to reveal more about customized software images.

You've confirmed you can run workloads via Azure Batch. In the next section, you'll sequence a genome with NGSEP. 