## Testing an Application

The TACC tool `idev` is used to start an interactive session on a Lonestar5 node. Interactive sessions are helpful to test code, debug code, and practice small jobs before submitting large jobs: 
```
$ idev --help
$ idev -p normal -m 180 --reservation=CTLS2017
```

Once your job begins, there will be a change in the command prompt and you can tell you are on a compute node. To test Tophat, we will download some test data and follow the instructions on the Tophat [website](https://ccb.jhu.edu/software/tophat/tutorial.shtml).
```
$ module load perl bowtie/2.2.6 cufflinks
 
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0   4) boost/1.59   5) samtools/1.3   6) perl/5.22.1   7) bowtie/2.2.6
```


```
$ cd /tophat/bin/dir # wherever you installed it
$ export PATH=$PWD:$PATH
 
$ cd /somewhere
$ wget https://ccb.jhu.edu/software/tophat/downloads/test_data.tar.gz
$ tar -xvzf test_data.tar.gz
$ cd test_data/
$ tophat -r 20 test_ref reads_1.fq reads_2.fq
``` 



Previous: [Installing an Application](hpc_software_environment_03.md) | Next: [Profiling an Application](hpc_software_environment_05.md)

