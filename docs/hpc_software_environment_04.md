## Testing an Application


 3. Test an application; idev; make test

The TACC tool `idev` is helpful for interactive session - running, testing jobs, etc.
```
$ idev --help
$ idev -p development
```

To test tophat:
```
$ module load perl bowtie/2.2.6
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0   4) boost/1.59   5) samtools/1.3   6) perl/5.22.1   7) bowtie/2.2.6
```
$ cd /tophat/bin/dir # wherever you installed it
$ export PATH=$PWD:$PATH

$ cd /somewhere
$ wget https://ccb.jhu.edu/software/tophat/downloads/test_data.tar.gz
$ tar -xvzf test_data.tar.gz
$ cd test_data/
$ tophat -r 20 test_ref reads_1.fq reads_2.fq
``` 


### Exercise

1. 

[Click here for solution](hpc_software_environment_04_solution.md)



Previous: [Installing an Application](hpc_software_environment_03.md) | Next: [Profiling an Application](hpc_software_environment_05.md)

