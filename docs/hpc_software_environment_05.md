## Profiling an Application

When running an application for the first time, it is useful to know how it behaves on a node. For example, how efficiently is it using the cores? How much memory does it use? How much I/O (input / output) does it do? Knowing these things, and others, can help the user determine the appropriate type of node, number of nodes, and even file system for running the application. 

TACC provides a job profiling tool called `remora`. It is extremely simple to use. On a compute node, navigate to your test Tophat data and perform the following:
```
$ module load remora
$ remora tophat -r 20 test_ref reads_1.fq reads_2.fq
```

The call to `remora` will create a new folder called blah, and output a summary to the screen. Closely examine the contents of the directory. How much RAM is required to run this small Tophat test?


Previous: [Testing an Application](hpc_software_environment_04.md) | Next: [Sharing an Application](hpc_software_environment_06.md)

