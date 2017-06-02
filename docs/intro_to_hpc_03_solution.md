1) Search the module system for any application(s) that you need for your research.

*For my research, I use a molecular dynamics tool called gromacs*:
```
$ module list
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0
 
$ module spider gromacs
---------------------------------------------------------------------------------------------------------
  gromacs:
---------------------------------------------------------------------------------------------------------
    Description:
      molecular dynamics simulation package
 
     Versions:
        gromacs/5.0.6
        gromacs/5.1.2
```


2) Figure out if any dependencies are required to load the module.
```
$ module spider gromacs/5.1.2       # carefully read output
...
    You will need to load all module(s) on any one of the lines below before the "gromacs/5.1.2" module is av
ailable to load.
 
      intel/16.0.1  cray_mpich/7.3.0
...
```

*It looks like I must have `intel/16.0.1` and `cray_mpich/7.3.0` loaded in order to load `gromacs/5.1.2`. I already have those loaded, so I should be ready to go.*


3) Load the module and determine what effect it has on your environment.
```
$ module show gromacs/5.1.2         # carefully read output
...
prepend_path("PATH","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/bin")
prepend_path("LD_LIBRARY_PATH","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/lib64")
setenv("TACC_GROMACS_DIR","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2")
setenv("TACC_GROMACS_INC","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/include")
setenv("TACC_GROMACS_LIB","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/lib64")
setenv("TACC_GROMACS_BIN","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/bin")
setenv("TACC_GROMACS_DOC","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/share")
setenv("GMXLIB","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/share/gromacs/top")
append_path("MANPATH","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/share/man")
append_path("PKG_CONFIG_PATH","/opt/apps/intel16/cray_mpich_7_3/gromacs/5.1.2/lib/pkgconfig")
...
```

*It looks like the major changes are to prepend the `PATH` and `LD_LIBRARY_PATH` environment variables, and to define several new variables with `_GROMACS_` in the name (plus a few other minor changes).*

```
$ echo $PATH
$ echo $TACC_GROMACS_DIR
$ module load gromacs/5.1.2
$ module list
$ echo $PATH
$ echo $TACC_GROMACS_DIR
```


4) Make sure the desired executables (and correct version) are in your PATH.
```
$ which gmx
# gmx --version       # do not run these applications on the login node, but checking the version is okay
```


[Return](intro_to_hpc_03.md)

