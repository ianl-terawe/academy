# Workspace Introduction

## DSVM Use 

Although this module is a logical continuation of the previous one, there is one compelling difference: for the purpose of genomic analysis, use is made here of a **virtual machine** (VM) on Azure. In other words, commands will be executed interactively via a Linux-based VM, as opposed to non-interactively via the Azure Batch service. The rationale for this change will become evident.

<!--- has it become eviudent? --->

Start by opening your **Workspace**. From the Workspace panel, you'll be able to retrieve the specifics needed to _connect_ to your VM via `ssh`. We encourage you to have a shell session on this VM _active_ as you work through the sections of this module. 

The VM you have accessed is running a **customized software image**. Built upon a relatively recent version of the Linux operating system (Linux Ubuintu 20.04), this image includes pre-installed software required for completion of this module. 

<!--- check O/S version --->

## X2Go Client 

X2Go installed on your computer with an open XFCE session. For more information, see [Install and configure the X2Go client](https://learn.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro#x2go). 

## Data Management 

Sorted BAM files (`CBS4C_sorted.bam` and `ER7A_sorted.bam`) and reference-genome files (`Saccharomyces_cerevisiae_STRs.txt` and `Saccharomyces_cerevisiae.fa`) from the first module are required as inputs for this module. Currently, these files reside in Azure blob storage. 

To make a copy of these files to the local file system on your VM, issue the command:

```bash
azcopy ???
```

To verify that the files were copied, the following Linux commands can prove useful:

- `du -h *` - provides a list of the files and their sizes in a human-readable form
- `file *` - provides a list of the files and their associated types 

<!--- include reference outputs for above commands? --->

Armed with a local copy of these critical files on your VM, you can proceed with next steps - namely, further analysis of the genomes sequenced in Module 1. 

## Jupyter Noteboook 

Open a Jupyter Notebook that connects to your Workspace. 

