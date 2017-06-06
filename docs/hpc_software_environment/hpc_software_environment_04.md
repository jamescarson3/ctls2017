## Testing an Application

We installed Tophat, now it is time to test it to make sure it is working. Revisting the [Tophat website](https://ccb.jhu.edu/software/tophat/tutorial.shtml), we find that they give instructions on how to test the code.

First, we will create a suitable place to test.
```
$ cd /work/03439/wallen/lonestar/apps/
$ mkdir tophat-test
$ cd tophat-test
```

Download and unpack the testing resources as described on the Tophat webiste:
```
$ wget https://ccb.jhu.edu/software/tophat/downloads/test_data.tar.gz
$ tar -xvzf test_data.tar.gz
$ cd test_data
$ ls -l
```

Since it is against policy to run applications on the login nodes, we must gain access to a compute node. The TACC tool `idev` is used to start an interactive session on a Lonestar5 compute node. Interactive sessions are helpful to test code, debug code, and practice small jobs before submitting large jobs: 
```
$ idev --help
$ idev -p normal -m 180 --reservation=CTLS2017
```


Check your environment to make sure you have the correct modules loaded still:
```
$ module list
Currently Loaded Modules:
  1) intel/16.0.1   2) cray_mpich/7.3.0   3) TACC/1.0   4) perl/5.22.1   5) bowtie/2.2.6   6) boost/1.59
```

We also have to put Tophat in our path. There is no module for Tophat yet, so we need to do it manually.
```
$ echo $PATH        
$ which tophat      # no tophat yet
$ export PATH=$PATH:/work/03439/wallen/lonestar/apps/tophat/2.1.1/bin
$ echo $PATH
$ which tophat      # tophat now in path
```

Finally, we will test Tophat interactively using the command provided on the tophat website:
```
$ tophat -r 20 test_ref reads_1.fq reads_2.fq
``` 

Carefully read the output to screen to make sure there are no errors. If everything worked, you should get output similar to the following:
```
$ cat tophat_out/align_summary.txt
Left reads:
          Input     :       100
           Mapped   :        72 (72.0% of input)
Right reads:
          Input     :       100
           Mapped   :        70 (70.0% of input)
71.0% overall read mapping rate.
 
Aligned pairs:        50
50.0% concordant pair alignment rate.
```

Previous: [Installing an Application](hpc_software_environment_03.md) | Next: [Profiling an Application](hpc_software_environment_05.md) | Top: [Course Overview](../../index.md)

