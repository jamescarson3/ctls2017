# Choosing the Correct Hardware

You may think that "bigger" or "faster" computers are automatically faster, but that is not always the case.
Each of our systems have their own unique strengths to serve specific types of computation loads.
No matter what you do, you know that specialized tools are better than others.

- Pipettes
- Sequencers
- Pens

Computers are exactly the same. Here is a condensed overview of some of our systems.

| System | Pros | Cons |
|--|--|--|
| Stampede | Thousands of nodes, Xeon Phi accelerators | Depreciated software stack and high demand |
| Stampede 2 | Thousands of nodes, KNL processors | Slow for serial code |
| Lonestar 5 | Compute, GPUs, Large-mem | UT only, slow external network |
| Wrangler | SSD Filesystem, Hosted Databases, Hadoop, HDFS | Low node-count |
| Jetstream | Long running instances, root access | limited storage |
| Maverick | GPUs, high memory | Depreciated software stack |
| Chameleon | GPUs, bare metal VM, software defined networking | Difficult to configure | 
| Catapult | FPGAs | Windows :D |
| Hikari | Protected Data | No scratch filesystem |

Just remember that after you choose a system, you should read the associated **user guide** to make sure know how to use its full potential.
I personally know that many people run on wrangler, but hardly anyone looks up the filesystem where the SSDs live.

In this course, you have been running on Lonestar 5.
This is a great general purpose system with GPUs and large-memory nodes.
You just have to submit to the correct queues to utilize them.
If you are associated with UT, you can request time on it for your projects without going through XSEDE.

### CPU bound code

Wikipedia defines code to be [CPU-bound](https://en.wikipedia.org/wiki/CPU-bound)

> when the time for it to complete a task is determined principally by the speed of the central processor.

This means that your program runtime should not significantly differ if your input comes from SSDs on Wrangler, or the tapes on Ranch.

![phant](http://www.smbc-comics.com/comics/20141022.png)

You can speed up CPU bound code by utilizing

- multiple cores (relatively simple)
  - pthreads
  - openmp
- multiple nodes
  - launcher
  - divide and conquer
  - MPI
- onboard accelerators (fairly difficult)
  - Xeon Phi
  - GPU
  - FPGA
  
Please consider attending one of our "many-core" or "mpi" workshops to learn how to program in these paradigms.

#### Explore

- Do you work with any CPU bound programs?
- Does the code utilize any of the listed technologies to shorten runtime?

### I/O bound code

Going back to [Wikipedia](https://en.wikipedia.org/wiki/I/O_bound), a code is called I/O bound if

> the time it takes to complete a computation is determined principally by the period spent waiting for input/output operations to be completed.

You can usually identify cases of slowdown caused by I/O when your processes are not utilizing an entire core.
This means that the code is either reading or writing a file and it has to STOP execution and wait for those file operations to finish.

To remove the I/O bottleneck, you first need to identify what kind of file operations your program performs.
At the very least, you may have pay attention to the files the program takes as input and produces, but you may also need to have an understanding of the code itself.

#### IOPS

If you code requires lots of IOPS, this usually means that it

- interacts with lots of files
  - Lots of intermediate files
  - Lots of output files
- randomly reads from files
  - Usually takes an index file
- randomly writes to files
  - rare
  - HDF5 file formats
  
You can speed up programs like these by

- reading and writing to `/dev/shm`
  - takes up main memory (RAM)
- reading and writing to `/tmp`
  - spinning disk, but you're the only one on it
  - larger than memory, but still limited
- using `/gpfs/flash` on wrangler
  - 500TB of flash!
  - No spinning disks

#### Throughput

If your code requires lots of throughput, it definitely reads and/or writes large (> 1GB) files.
Running multiple processes will oversaturate the link to the filesystem and actually slow things down.
Luckily, Lustre ($SCRATCH, $WORK) is ideal for this kind of workload.

When you find that your program is being slowed down, you can try the following things

- Compress input/output
  - cmd | gzip -c - > out.gz
  - gzip -dc input.gz | cmd
  - Uses more processor power for smaller files
- Use more files
  - Lustre is a distributed filesystem, so a single process can max out a single storage server. Writing multiple files will help distribute that load.

#### File count

Lastly, your code can slow down based on how many files your code reads or writes.
We previously recommended that you could circumvent throughput bottlenecks by writing multiple files, but if you make too many files, simple `ls` commands could overload the Lustre metadata servers.
The Trinity transcriptome assembly is guilty of this.

If you notice that your program is making huge numbers of files, you can try

- Writing to `/dev/shm` or `/gpfs/flash`
  - `tar` the output to $WORK after running
- Write to multiple directories
  - This is what we do with $HOME, $WORK, and $SCRATCH
- Clean up files as you go

### Explore

- Can you think of any I/O bound programs?
- Try using some of our recommended solutions to speed up your code
  - Let us know if you would like to try using Wrangler this week
- Try running the tophat example in shared memory
<br>
<br>

[Back - Optimization](optimization_parallelization_05.md)
&nbsp;&nbsp;&#151;&nbsp;&nbsp;
[Next - Agenda](../../index.md)
