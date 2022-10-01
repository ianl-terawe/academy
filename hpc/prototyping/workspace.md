
# Workspace 

## Accessing the Cloud-Based Windows Desktop 

<!--- RDP on other non-Windows platforms --->

Open your Workspace. Note that the RDP file contains the details required to connect to your Windows-based desktop on Azure. 

If you are making use of a Windows desktop, download the RDP file. Double-clicking on this file will result in the desktop experience illustrated below - once you've entered your login and password details. Use will be made of this desktop throughout this module. 

![oneAPI desktop](https://raw.githubusercontent.com/ianl-terawe/academy/main/hpc/prototyping/media/oneAPIdesktop.png "oneAPI desktop")

If your desktop is macOS or Linux based, you'll need to install an RDP client before you can made use the cloud-based Windows desktop. 

<!--- Please refer to ??? for an RDP client appropriate for your laptop or desktop. --->

## HPC-Customized Software Image 

This desktop introduces you to the Intel oneAPI toolchain on Microsoft Windows. To ensure the environment is a functional one from the development perspective, the desktop includes:

- The Intel oneAPI toolchain 
- Microsoft Visual Studio to serve the role of an IDE (Integrated Development Environment)
- Tools to facilitate interaction with GitHub 

<!--- Visual Studio - license needed? --->

As the emphasis of this module is HPC, the toolchain features the [Intel® oneAPI HPC Toolkit](https://www.intel.com/content/www/us/en/developer/tools/oneapi/hpc-toolkit.html). This HPC Kit includes:

- Compilers - from both classic and oneAPI C/C++ to Fortran
- Libraries - to support shared (via OpenMP) and distributed-memory (via MPI) parallel computing 
- Tools - from debuggers and profilers to those that target excution environments (e.g., clusters)

> **Note:**
> The Intel® oneAPI HPC Toolkit is an add-on to the Intel® oneAPI Base Toolkit. Consequently, to enable full functionality, the base toolkit has also been pre-installed into the Workspace you are using on this desktop. 

<!--- gcc use --->

## Next Steps 

As your cloud-based Windows desktop is ready use with the Intel toolchain, you can proceed directly to making use of code samples. 