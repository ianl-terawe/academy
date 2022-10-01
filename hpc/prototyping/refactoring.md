# Refactoring for oneAPI 

# Implications 

Embracing the latest XPU offering can have serious implications at the source-code level – far too often requiring that code be refactored. GROMACS, illustrates this point exceedingly well. Originally written some 30 years ago in Fortran, GROMACS was systematically rewritten in the C programming language and ultimately in C++. Over this timeframe, the community responsible for GROMACS development has fashioned implementations to target processors ranging from modest to many-core CPU architectures to other classes of XPUs. To support GPUs, for example, use of proprietary languages (e.g., CUDA) has been a requirement; although this may result in a processor-specific implementation that is performant, the resulting code is vendor-locked (i.e., anything but portable). 

The GROMACS community has been exceptional in ‘evolving’ their application, as refactoring code is a labor-intensive undertaking – especially when thousands of lines of code are involved. In other words, for most HPC applications, refactoring for each new class or even generation of XPUs borders on the impractical. 

# GROMACS and the Case for oneAPI 

The transition at the source-code level to C++ has proven to be a worthwhile investment for GROMACS. As the history of GROMACS implementations demonstrates, advancements in HPC technology have motivated advancements in the application; more importantly, however, is the fact that many of these technological enhancements have necessitated refactoring at the source-code level. In some cases then, substantial refactoring and reimplementation has been called for. The effort involved here can be concerning as scientists and engineers become ‘distracted’ by IT from their primary interests. 

Often the root cause is the introduction of a ‘new’ processor. In this regard, even new generations of CPUs have proven ‘disruptive’ – again, a reality captured via the history of GROMACS implementations.

The GROMACS community has become early adopters of oneAPI; in fact, only a single flag needs to be added (-DGMX_GPU=SYCL) to make use of the Intel oneAPI toolchain (i.e., Intel oneAPI DPC++).

It is important to highlight the impact of oneAPI for applications such GROMACS – i.e., applications comprised of thousands of lines of source code. By adopting oneAPI, as the GROMACS community has, recompilation is all that is required to take advantage of the latest XPU offering. To be clear: there is no need to refactor at the source code level. This is a significant advantage for the application, as it rapidly accelerates uptake of the latest XPU offerings in support of scientists’ and engineers’ GROMACS use cases. Stated succinctly, XPU-neutral oneAPI obviates the proliferation of the processor landscape as a challenge for GROMACS. Or, from the opposite perspective, uptake of oneAPI introduces the breadth and depth of the XPU landscape as opportunities for GROMACS use cases. 