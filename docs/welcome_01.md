# Welcome to Computational Techniques for Life Sciences

## Agenda Today

| Time | Topic |
|--------|--------------------------------------------------|
|  8:30 - 10:00 | [Welcome / Introduction to Linux](docs/intro_to_linux.md) |
| 10:00 - 10:15 | Break |
| 10:15 - 11:45 | Introduction to High Performance Computing |
| 11:45 - 13:00 | Lunch |
| 13:00 - 14:30 | Useful Command Line Utilities |
| 14:30 - 14:45 | Break |
| 14:45 - 17:00 | Hand-on Exercises & Bring-your-own-code Workshop |

## Getting Set Up

Please log in to the WiFi:

```
  Network - TACC
  Username - username
  Password - password
```

Please log in to the Lonestar5 cluster (Mac / Linux):

```
  Open the application 'Terminal'
  ssh username@ls5.tacc.utexas.edu 
  (enter password)
  (enter 6-digit token)
```

Please log in to the Lonestar5 cluster (Windows):

```
  Open the application 'PuTTY'
  enter Host Name: ls5.tacc.utexas.edu
  (click 'Open')
  (enter username)
  (enter password)
  (enter 6-digit token)
```



PAGE BREAK HERE 



## Objectives for the Computational Techniques for Life Sciences Summer Institute

 Provide attendees the basic skills needed to:

 1. Execute life sciences workflows on large-scale systems
 2. Run parallel analyses
 3. Use Bash/Python/Perl to chain common life sciences applications together to form more complex workflows
 4. Analyze and visualize result data in order to gain useful insights



## What is the Texas Advanced Computing Center?

But first, a little about us:

 * We are a research center at UT Austin
 * ~160 Staff, 85% funding from external grants
 * We support over 10,000 users on ~2,300 active projects

<center> *Mission: "To enable discoveries that advance science and society through the application of advanced computing technologies."*</center>


<center><img src="https://github.com/jamescarson3/ctls2017/blob/master/resources/machines.png" style="height:300px;"></center>



## Basic High Performance Computing (HPC) System Architecture

As we log in and prepare to use Lonestar5, it is important to understand the basic architecture. Think of an HPC resource as a very large and complicated lab instrument. Users need to learn how to:

 * Interface with it / push the right buttons (Linux)
 * Load samples (data)
 * Run experiments (jobs)
 * Interpret the results


<center><img src="https://github.com/jamescarson3/ctls2017/blob/master/resources/hpc_schematic.png" style="height:300px;"></center>


**Read the documentation.**

 * Learn node schematics, limitations, file systems, rules
 * Learn about the scheduler, queues, policies
 * Determine the right resource for the job

HPC systems are shared resources. Your jobs and activity on a cluster, if mismanaged, can affect others. TACC staff are always [available to help](https://portal.tacc.utexas.edu/tacc-consulting).


&copy; 2017 Texas Advanced Computing Center

