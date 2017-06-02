1) Assuming you put `blast/2.2.31` into your default modules using `module save`, how do you undo that change?

```
$ module list
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0   4) blast/2.2.31
 
$ module unload blast
$ module list
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0
 
$ module save
```

*Log out and log back in to see if it worked.*

[Return](intro_to_hpc_04.md)

