
1) Try loading gcc and intel compilers at the same time. What happens?
```
$ module list
  
  Currently Loaded Modules:
    1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0
  
$ module load gcc
  Lmod is automatically replacing "intel/16.0.1" with "gcc/5.2.0".
  
  Due to MODULEPATH changes, the following have been reloaded:
    1) cray_mpich/7.3.0
  
$ module list
  
  Currently Loaded Modules:
    1) TACC/1.0   2) gcc/5.2.0   3) cray_mpich/7.3.0
```

*Having both intel and gcc compilers loaded would be a conflict, so the module system does not allow it.*

2) Determine recommended compiler / dependencies for a software package you use. Are they available on Lonestar5?

*As an example application, we will consider [Tophat](https://ccb.jhu.edu/software/tophat/tutorial.shtml). Listed on the Tophat website are the following dependencies: `bowtie`, `boost`
```
$ module avail bowtie
$ module avail boost
```

[Return](hpc_software_environment_02.md)

