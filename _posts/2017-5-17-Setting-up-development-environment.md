So, as such I had previously compiled and built hpx, hpxcl for Windows with Visual Studio 2015 during the proposal phase of GSoC.

Now, I need will be shifting development machine and will not be having a laptop with cuda compatability for a brief period of time. So, I need to be able to write code on my development machine and run it on Rostam in the mean-time. Since I need to be able to make sure, the code builds properly, I needed to install in my development Machine (Windows and Ubuntu on Windows) and Rostam.

Installing HPX on Windows
---------------------------

It is necessary to ensure that all the pre-requisites of the project are installed first and are discoverable.

**Boost** can be downloaded from the official repository. SInce non-static libraries are to be used for HPX, we need to build and install the non-static libraries of boost. Installation of boost can be done by following this [blog](https://codeyarns.com/2014/06/06/how-to-build-boost-using-visual-studio/). It is imperative to keep the compiler in mind, as multiple Visual C++ run-time could be installed on the machine and only the same must be used for boost installation and in Visual Studio. For example, if we are to use Visual Studio 2015, which usually uses MSVC 14.0, then  the same must be used for boost.

**Hwloc** is the hardware locality library for MPI. The appropriate libraries can just be used from the website. HWLOC_ROOT can be configured accordingly.

Currently, the 64-bit build of the code is successful, hkaiser is working on the 32-bit build.

Building HPXCL on Windows
------------------------------
Since the development of HPXCL, would require the appropriate opencl and cuda libraries, the same needs to be downloaded.

Using NVIDIA Graphics card, the NVIDIA Toolkit encompasses the required libraries for both opencl and cuda. CUDA is only compatible on NVIDIA Graphics card.

While using Graphics Card from other vendors, the appropriate OpenCL libraries need to be downloaded separately and installed. HPXCL will then find the OpenCL libraries based on the environment automatically. I made this change in the CMakeLists file on the [Pull Request](https://github.com/STEllAR-GROUP/hpxcl/pull/43).

Installing HPX on Rostam
---------------------------------
All the pre-requisites are previously installed on Rostam, and usually multiple versions of the same.

The appropriate versions of the libraries can be loaded using a command similar to the following,

```
module load cmake/3.7.2 gcc/6.3.0 boost/1.63.0-gcc6.3.0

```

Then HPX can be installed normally by issuing make install.