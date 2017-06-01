## Lonestar5 Basics

 1. Navigate Lonestar5 effectively; identify compilers and dependencies

<center><img src="../resources/lonestar.jpg" style="height:300px;"></center>

### Architecture

 * 1252 24-core general compute nodes (~30K cores total)
 * 16 GPU nodes
 * 10 large memory nodes
 * 80 TB memory, 5 PB disk storage, 1.2 PF peak performance

Login nodes:

 * Dual Socket
 * Xeon CPU E5-2650 v3 (Haswell): 10 cores per socket (20 cores/node), 2.30GHz
 * 128 GB DDR4-2133
 * Hyperthreading Disabled

Compute Nodes

 * Dual Socket
 * Xeon E5-2690 v3 (Haswell) : 12 cores per socket (24 cores/node), 2.6 GHz
 * 64 GB DDR4-2133 (8 x 8GB dual rank x8 DIMMS)
 * No local disk
 * Hyperthreading Enabled - 48 threads (logical CPUs) per node


### File Systems

You have access to the following spaces (5-digit lustre number and username vary for each user):
```
/home1/03439/wallen/      # 5 GB quota
/work/03439/wallen/       # 1 TB quota
/scratch/03439/wallen/    # unlimited quota, but subject to purge
```

Shortcuts to switch between the three spaces are:
```
$ cd
$ cdw
$ cds
```

Or:
```
$ cd $HOME
$ cd $WORK
$ cd $SCRATCH
```

### Compilers

To identify available gcc and intel compilers, try:
```
$ module spider gcc
...
  Versions:
     gcc/4.9.3
     gcc/5.1.0
     gcc/5.2.0
...
$ module spider intel
...
  intel: intel/16.0.1
...
```

Loading a gcc module will put the compilers `gcc`, `g++`, and `gfortran` in your path.

Loading an intel module will put the compilers `icc`, `icpc`, and `ifort` in your path.

For MPI programming, the MPICH implementation of the MPI standard is available as:
```
$ module spider cray_mpich
```

Loading this module will put the compilers `mpicc`, `mpicxx`, and `mpif90` in your path.


### Common Dependencies
```
$ module spider mkl
$ module spider fftw
$ module spider hdf5
$ module spider cmake

```



### Exercise

1. Try loading gcc and intel compilers at the same time. What happens?
2. Determine recommended compiler / dependencies for a software package you use. Are they available on Lonestar5?

[Click here for solution](hpc_software_environment_02_solution.md)



Previous: [HPC Software Environment](hpc_software_environment_01.md) | Next: [Installing an Application](hpc_software_environment_03.md)

