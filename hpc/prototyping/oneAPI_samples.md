# Running oneAPI Code Samples 

## oneAPI Code Samples 

Your ManageX Academy Workspace is a Windows-based desktop on Azure. This cloud-based Windows desktop comes pre-loaded with everything you need to prototype HPC application development - i.e., author/edit, compile/link, and run code.

To get started, open Microsoft Visual Studio and click `Continue without code`. 

From Visual Studio's top menu, select `Extensions > Intel > Browse Intel oneAPI Samples` to see the samples screen:

<!--- replace screenshot --->

![oneAPI samples screen](/hpc/prototyping/media/oneAPIsamplesscreen.png "oneAPI samples screen")

For a video from Intel on the samples browser see:

[![oneAPI samples screen video](/hpc/prototyping/media/oneAPIsamplesscreen.png "oneAPI samples screen video")](https://youtu.be/_0qTBthNkSM)

## Running a Matrix-Mutiplication Sample 

After selecting `Get Started`, highlight `Matrix Mul`, and click `OK`. 

As you'd expect, this sample involves the multiplication of matrices. It is implemented in a combination of DPC++ and OpenMP. The Visual Studio interface highlights the code syntax for you. This will allow you to rapidly identify unfamiliar synatx relating to DPC++ itself, for example. 

From the `Solution Explorer`, right click on `matrix_mul_mkl` and select `Rebuild`.

From the top menu, select `DebugStart Without Debugging`. The debug results will appear in the debug console. Refer to the screenshot below:

![oneAPI samples - matrix multiplication](/hpc/prototyping/media/oneAPIsamples_runmatmult.png "oneAPI samples - matrix multiplication")

> **Note:**
> This example draws heavily upon developer-centric content from Intel; you can find that resource [here](https://www.intel.com/content/www/us/en/develop/documentation/get-started-with-intel-oneapi-hpc-windows/top/run-a-sample-project-with-visual-studio.html). Consult this resource for additional details regarding this example. 

## Other oneAPI Code Samples and More 

The HPC Kit from Intel includes numerous code samples that make use of oneAPI. oneAPI libraries and tools are also included. 

Using the same approach as above (i.e., in the case of the matrix-multiplication example), you may explore additional oneAPI code samples. 

## Learning to Program for oneAPI 

These samples should encourage and inform your uptake of oneAPI. However, many learners will require a more-formal introduction. Fortunately, there are numerous resources available; for example:

- [oneAPI's home page](https://www.oneapi.io/)
- [Intel's developer-centric offering](https://www.intel.com/content/www/us/en/developer/tools/oneapi/overview.html)