In this post, I shall compare and contrast the different benchmarking tools available for Benchmarking GPU Devices running CUDA and OpenCL. The main aim is to be able to make an informed decision about the benchmarks to be selected for testing HPXCL.

SPEC ACCEL (Standard Performance Evaluation Corporation for Accelerators)
-----------------------------
(For benchmarking OpenCL)

Derived from Parboil Benchmark from the IMPACT Research Group of University of Illinois at Urbana-Champaign. [2]

Features:
1. Runs under OpenCL and OpenACC APIs.
2. Measures performance of accelerator, host CPU, memory transfer between host and accelerator, other drivers and libraries.
4. Provide 19 tests for OpenCL enabled benchmarking and 15 for OpenMP enabled benchmarking.

Disadvantages:
1. No Support for OpenMP version 4.0, not relevant for benchmarking HPXCL.
2. Benchmarks the paralellism acheieved between nodes or with OpenCL and not both together.
3. Need to test varying loads of data.

Lulesh (Livermore Unstructured Lagrangian Explicit Shock Hydrodynamics) 
------------------------
(CUDA and OpenCL)

Lulesh Benchmark was co-designed as Lawrence Livermore National Lab.

LULESH is a highly simplified application, hard-coded to only solve a simple Sedov blast problem with analytic answers – but represents the numerical algorithms, data motion, and programming style typical in scientific C or C++ based applications. [1]

Features:
1. Both OpenCL and CUDA versions available.
2. Contains three main kernels of Hexahedron Volume Calculation, Force Calculation and Calculate linear and quadratic artificial viscosity coefficients.


HPCChallenge
--------------------
(Not applicable for HPXCL)

This benchmark is used for the testing a number of independent attributes of the performance of High Performance Computer (HPC) Systems. Project sponsored by DARPA High Productivity Computing Systems program, United States Department of Energy and the National Science Foundation.

Features:
1. Used for benchmarking HPC systems.
2. Assumes System under test is a cluster of shared memory multi-processor systems connected to a network.
3. Runs with different modes of operation, nodes, for instance single (randomly selected node on a cluster), star (independent copy of results were run concurrently) and global (processors were working in coordination)

Disadvantages
1. Cannot be used for benchmarking HPXCL and it does not use GPUs.


References:
-------------------
[1] Livermore Unstructured Lagrangian Explicit Shock Hydrodynamics (LULESH). Retrieved from: [https://codesign.llnl.gov/lulesh.php](https://codesign.llnl.gov/lulesh.php) on: 20 June 2017
[2] The Standard Performance Evaluation Corporation (SPEC). Retrieved from: [http://www.spec.org/](http://www.spec.org/) on: 20 June 2017
