## Batch Job Submission

Example slurm script called, for example, `job.slurm`:
```
#!/bin/bash
#SBATCH -J myMPI            # job name
#SBATCH -o myMPI.o%j        # output and error file name (%j expands to jobID)
#SBATCH -N 2                # number of nodes requested
#SBATCH -n 48               # total number of mpi tasks requested
#SBATCH -p development      # queue (partition) -- normal, development, etc.
#SBATCH -t 01:30:00         # run time (hh:mm:ss) - 1.5 hours

# Slurm email notifications are now working on Lonestar 5 
#SBATCH --mail-user=username@tacc.utexas.edu
#SBATCH --mail-type=begin   # email me when the job starts
#SBATCH --mail-type=end     # email me when the job finishes

# run the executable named a.out
ibrun ./a.out               
```



Submit a job to the queue:
```
$ sbatch job.slurm
```

View the jobs you have currently in the queue:
```
$ showq -u
$ showq      # shows all jobs by all users
```

Cancel a running job:
```
$ scancel jobid
```

Run an interactive job:
```
$ idev --help
```

For more example scripts, see:
```
/share/doc/slurm/
```





### Other Considerations:

READ THE DOCUMENTATION
Learn the node schematics, limitations, file systems, rules
Learn the scheduler, queues, policies

HPC systems are shared resources. Your jobs, if mismanaged, can affect others.

Do not copy a job submission script from one resource to another. Build from scratch or from system example.

Practice, practice, practice.




### Exercise

1. Blah

[Click here for solution](intro_to_hpc_05_solution.md)

### Review of Topics Covered

| Command             | Effect     |
|---------------------|------------|
| `sbatch job.slurm`  | submit batch job called "job.slurm" |
| `showq`             | show all running and queued jobs |
| `showq -u`          | show all running and queued jobs by this user |
| `scancel jobid`     | cancel a job with id "jobid" |
| `idev --help`       | show idev help text for running interactive jobs |



Previous: [The .bash_profile](intro_to_hpc_04.md) | Return to [Agenda](../index.md)
