## Profiling an Application

When running an application for the first time, it is useful to know how it behaves on a node. For example, how efficiently is it using the cores? How much memory does it use? How much I/O (input / output) does it do? Knowing these things, and others, can help the user determine the appropriate type of node, number of nodes, and even file system for running the application. 

TACC provides a job profiling tool called `remora`. It is extremely simple to use. On a compute node, navigate to your test Tophat data and perform the following:
```
$ module load remora
$ remora tophat -r 20 test_ref reads_1.fq reads_2.fq
...
=============================== REMORA SUMMARY ===============================
 Max Memory Used Per Node     : 0.28 GB
 Total Elapsed Time           : 0d 0h 0m 2s 177ms
------------------------------------------------------------------------------
 Max IO Load / scratch        :       0 IOPS       0 RD(MB/S)       0 WR(MB/S)
 Max IO Load / work           :       0 IOPS       0 RD(MB/S)       0 WR(MB/S)
/opt/apps/remora/1.7/bin/aux/report: line 127: printf: ---: invalid number
 Max IO Load / apps           :       0 IOPS     --- RD(MB/S)         WR(MB/S)
/opt/apps/remora/1.7/bin/aux/report: line 127: printf: ---: invalid number
 Max IO Load / home1          :       0 IOPS     --- RD(MB/S)         WR(MB/S)
/opt/apps/remora/1.7/bin/aux/report: line 127: printf: ---: invalid number
 Max IO Load / repl           :       0 IOPS     --- RD(MB/S)         WR(MB/S)
/opt/apps/remora/1.7/bin/aux/report: line 127: printf: ---: invalid number
 Max IO Load / tacc           :       0 IOPS     --- RD(MB/S)         WR(MB/S)
==============================================================================
 Sampling Period              : 10 seconds
 Complete Report Data         : /work/03439/wallen/lonestar/apps/tophat-test/test_data/remora_865171
==============================================================================
...
```

This particular test Tophat job is very fast - only requiring approximately 2 seconds. So, profiling this job is not particularly useful, although it does provide a look at what sort of output we can expert. The `remora` wrapper creates a new directory called `remora_865171/`, where the 6-digit number is the same as your current jobid. Navigate into that directory, then into the `MEMORY` sub directory. Examing the contents of `memory_all_nodes.txt`:
```
$ cd remora_865171/MEMORY/
$ cat 
#HOST     VIRT_MAX  RES_MAX  FREE_MIN
nid00019 0.2765 0.0255 60.1907
```

There is only one time point shown, as the sampling window for remora (10s) is much longer than the time required to run this job (2s). But, this timepoint shows that about a quarter of a GB of memory was in use during job execution.


Previous: [Testing an Application](hpc_software_environment_04.md) | Next: [Sharing an Application](hpc_software_environment_06.md) | Top: [Course Overview](../../index.md)

