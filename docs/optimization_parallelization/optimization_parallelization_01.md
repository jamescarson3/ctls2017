# Optimization/Parallelization of Workflows for HPC

At TACC and CyVerse, we assume the software we serve will be run

- by significant portions of the community
- on always larger datasets
- by users with a diverse background

So we strive to not only deliver functional tools, but also tools that are tuned to run as efficiently as possible on our hardware.
This type of work is started by the HPC group at TACC, where they tune the compilers, system libraries, and communication stack on each system.
The Life Sciences group will then build our applications from this base environment to provide the best tools possible.

Time - 90 minutes

### Questions
* Does my analysis efficiently utilize resources?

### Objectives
* Monitor a job to evaluate performance.
* Break down a large task into multiple small tasks.
* Optimize code for a specific architecture.
* Use the optimal resources for your problem.

# Topics Covered

- Monitoring jobs - (`top`, `time`, `remora`)
- Parallelization - (`threading`, `for/wait`, `xargs`)
- Distribution - (`launcher`)
- Code Optimization - (optimization, vectorization)
- Choosing hardware - (io, cpu, memory)
<br>
<br>

[Back - Agenda](../../index.md)
&nbsp;&nbsp;&#151;&nbsp;&nbsp;
[Next - Monitoring Jobs](optimization_parallelization_02.md)
