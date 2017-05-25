# Introduction to High Performance Computing

## Module Objectives

This module will be fully interactive. Participants are **strongly encouraged** to follow along on the command line. After taking this module, participants should be able to:

 * Print, identify, and modify environment variables
 * List and search for available modules
 * Load and unload modules specific to a certain objective
 * Automate module and environment commands in the `.bash_profile`
 * Prepare and submit a batch job to a queue



## Basic High Performance Computing (HPC) System Architecture

### Quick Reminder:

<center><img src="../resources/hpc_schematic.png" style="height:300px;"></center>


### Tips for Success:

*Read the documentation.*

 * Learn node schematics, limitations, file systems, rules
 * Learn about the scheduler, queues, policies
 * Determine the right resource for the job

HPC systems are shared resources. Your jobs and activity on a cluster, if mismanaged, can affect others. TACC staff are always [available to help](https://portal.tacc.utexas.edu/tacc-consulting).


## Topics Covered:

 * Environment variables – purpose, printing, and defining (`echo, env, export`).
 * Modules – listing, loading, and unloading.
 * Automating environment variables, module commands, and aliases in `.bash_profile`.
 * Batch job submission, commands dependent on system (`qsub, showq, qdel`).


Next: [Environment Variables](intro_to_hpc_02.md)


