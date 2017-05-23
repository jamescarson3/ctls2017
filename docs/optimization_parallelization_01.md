# Optimization/Parallelization of Workflows for HPC

Time - 90 minutes

### Questions
* Does my analysis efficiently utilize resources?

### Objectives
* Monitor a job to evaluate performance.
* Break down a large task into multiple small tasks.
* Optimize code for a specific architecture.
* Use the optimal resources for your problem.

## Monitoring a Job

- `top`
- `time`
- `remora`

## Parallelization and Distribution

- threading
   - general programs
   - python
   - R
- `awk`
- for -> wait
- make -> makeflow
- launcher
- split -> launcher -> merge

## Code Optimization

- affinity
- vectorization
- mkl

## Matching Software to Hardware

- i/o
   - `/dev/shm`
   - Wrangler
- cpu
   - single thread
   - multithread
- GPU
   - Maverick
