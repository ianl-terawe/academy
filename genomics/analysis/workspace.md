# Workspace Introduction

## Virtual Machine Use 

Although this module is a logical continuation of the previous one, there is one compelling difference: for the purpose of genomic analysis, use is made here of a **virtual machine** (VM) on Azure. In other words, commands will be executed interactively via a Linux-based VM, as opposed to non-interactively via the Azure Batch service. The rationale for this change will become evident.

Start by opening your **Workspace**. From the Workspace panel, you'll be able to retrieve the specifics needed to _connect_ to your VM via `ssh`. We encourage you to have a shell session on this VM _active_ as you work through the sections of this module. 

The VM you have accessed is running a **customized software image**. Built upon a relatively recent version of the Linux operating system, this image includes pre-installed software required for completion of this module. 