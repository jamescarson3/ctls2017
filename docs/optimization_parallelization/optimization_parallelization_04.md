# Task Distribution

One of the most convenient tools that we have at TACC is [Launcher](https://github.com/TACC/launcher). Similar to `xargs`, Launcher is a simple way to work through single-node tasks. In addition to scheduling tasks on a single node, Launcher can also spawn tasks on other nodes allocated to the job. This is good news for everyone that needs to complete a lot of work because every time you submit a job, your priority goes down. If you can bundle all of your work into one large job, you will optimize your scheduling priority.

Launcher works by working through a text file and executing each line as a job. Inside each line

- Output can be piped
- Commands can be chained
- `if/else` works
- Your original environment is preserved

Lets begin by making a program that writes the task ID and the hostname it was run from.

```
for ID in {1..48}
do
   echo "echo $ID - "'$HOSTNAME - $(date +%s)'
done
```

If all the quotes are correct, your output should look like

```
echo 1 - $HOSTNAME - seconds
echo 2 - $HOSTNAME - seconds
...
echo 47 - $HOSTNAME - seconds
echo 48 - $HOSTNAME - seconds
```

Redirect this to a file so we can run it with launcher.

```
for ID in {1..48}
do
   echo "echo $ID - "'$HOSTNAME - $(date +%s)'
done > launcher_cmds.txt
```
### Single node tasks

Using the skills we already have, we can already run this file in parallel on a single node using `xargs`.

```
cat launcher_cmds.txt | xargs -L 1 -P 3 -I {} bash -c {}
```

We can turn this into a launcher job by creating the SLURM submission script `launcher_single.sh`

```
#SBATCH -J hostname      # Job name
#SBATCH -o hostname.%j.o # Name of stdout output file (%j expands to jobId)
#SBATCH -e hostname.%j.e # Name of stdout output file (%j expands to jobId)
#SBATCH -p normal        # Queue name
#SBATCH -N 1             # Total number of nodes requested (24 cores/node)
#SBATCH -n 24            # Total number of tasks to run in total
#SBATCH -t 00:10:00      # Run time (hh:mm:ss)
#SBATCH -A TRAINING-HPC  # <-- Allocation name to charge job against

# Load launcher
module load launcher

# Configure launcher
EXECUTABLE=$TACC_LAUNCHER_DIR/init_launcher
PRUN=$TACC_LAUNCHER_DIR/paramrun
CONTROL_FILE=launcher_cmds.txt
WORKDIR=.

# Start launcher
$PRUN $EXECUTABLE $CONTROL_FILE
```

Then submit the job script to your reservation

```
sbatch --reservation=LSC launcher_single.sh
```

This job will run all 48 tasks in parallel 24 at a time (`-n 24`) on a single node (`-N 1`). If your tasks require multiple cores, make sure you divide `-n` by that number. For example, use `-n 4` to concurrently run 4 6-core tasks on all 24 cores on a LS5 compute node.

#### Explore

- Try using launcher with other code you know
- Try monitoring a launcher job with remora

### Running tasks on multiple nodes

Whenever you workload becomes too large for a single node, Launcher makes it easy to run it across more, and TACC always has more nodes. All you need to do is increase `-N` to reflect the number of nodes you need, and set `-n` to equal `tasks_per_node * N`.

Lets give it a try with our example.

```
#SBATCH -J host_dist      # Job name
#SBATCH -o host_dist.%j.o # Name of stdout output file (%j expands to jobId)
#SBATCH -e host_dist.%j.e # Name of stdout output file (%j expands to jobId)
#SBATCH -p normal        # Queue name
#SBATCH -N 2             # Total number of nodes requested (24 cores/node)
#SBATCH -n 48            # Total number of tasks to run in total
#SBATCH -t 00:10:00      # Run time (hh:mm:ss)
#SBATCH -A TRAINING-HPC  # <-- Allocation name to charge job against

# Load launcher
module load launcher

# Configure launcher
EXECUTABLE=$TACC_LAUNCHER_DIR/init_launcher
PRUN=$TACC_LAUNCHER_DIR/paramrun
CONTROL_FILE=launcher_cmds.txt
WORKDIR=.

# Start launcher
$PRUN $EXECUTABLE $CONTROL_FILE
```

Submit it to the same reservation

```
sbatch --reservation=LSC launcher_single.sh
```

Use `squeue -u username` to watch the progress of your job.
Then look at the output when it finishes.

```
less host_dist*.o
```

You should see two distinct host names in your output.

You are now ready to utilize multiple nodes for your work at TACC.
Launcher makes it that (relatively) easy.

### Running sort on two nodes

Lets write a workflow to sort two bed files concurrently. First, copy the bed files to your `$SCRATCH` directory.

```
$ cd $SCRATCH
$ cp /work/03076/gzynda/public/data/ctls2017/* .
```

You should now see two large BED files with SRA naming.

- SRR1570041.bed
- SRR2014925.bed

#### Command file

Now that you have your input files, we need to create the launcher command file.
Please adapt the following command for both files.

```
sort --parallel 24 -S 100M -k1,1 -k2,2n IN.bed > OUT.bed
```

Your command file shold have two lines!

#### Write a new submission file

You now need to modify your SLURM submission file to use the new command file.

```
cp launcher_single.sh launcher_sort.sh
```

Now edit `launcher_sort.sh`

```
#SBATCH -J host_dist      # Job name
#SBATCH -o host_dist.%j.o # Name of stdout output file (%j expands to jobId)
#SBATCH -e host_dist.%j.e # Name of stdout output file (%j expands to jobId)
#SBATCH -p normal        # Queue name
#SBATCH -N 2             # Total number of nodes requested (24 cores/node)
#SBATCH -n HOWMANY??            # Total number of tasks to run in total
#SBATCH -t 00:10:00      # Run time (hh:mm:ss)
#SBATCH -A TRAINING-HPC  # <-- Allocation name to charge job against

# Load launcher
module load launcher

# Configure launcher
EXECUTABLE=$TACC_LAUNCHER_DIR/init_launcher
PRUN=$TACC_LAUNCHER_DIR/paramrun
CONTROL_FILE=[CHANGE THIS!!!!]
WORKDIR=.

# Start launcher
$PRUN $EXECUTABLE $CONTROL_FILE
```

#### Submit!

Everything should work if you submit.

#### Explore

- Craft your own multi-node scripts for some of your tools

### Launcher Limitations

Launcher is great, but it has two limitations that you may eventually run into.

- It cannot dynamically add tasks to its work queue
- All commands are executed in the `sh` (Bourne) shell, not `bash`
<br>
<br>

[Back - Parallelization](optimization_parallelization_03.md)
&nbsp;&nbsp;&#151;&nbsp;&nbsp;
[Next - Optimization](optimization_parallelization_05.md)
