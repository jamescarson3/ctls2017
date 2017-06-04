# Task Distribution

One of the most convenient tools that we have at TACC is [Launcher](https://github.com/TACC/launcher). Similar to `xargs`, Launcher is a simple way to to work through single-node tasks. In addition to scheduling tasks on a single node, Launcher can also spawn tasks on other nodes allocated to the job. This is good news for people that need to complete a lot of work because every time you submit a job, your priority goes down. If you can bundle all of your work into one large job, you will optimize your scheduling priority.

Launcher works by working through a text file and executing each line as a job. Inside each line

- Output can be piped
- Commands can be chained
- `if/else` works
- Your original environment is preserved

Lets begin by making a program that writes the task ID and the hostname it was run from.

```
for ID in {1..48}
do
   echo "echo $ID - "'$HOSTNAME'
done
```

If all the quotes are correct, your output should look like

```
echo 1 - $HOSTNAME
echo 2 - $HOSTNAME
...
echo 47 - $HOSTNAME
echo 48 - $HOSTNAME
```

Redirect this to a file so we can run it with launcher.

```
for ID in {1..48}
do
   echo "echo $ID - "'$HOSTNAME'
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
#SBATCH -A CTLS2017      # <-- Allocation name to charge job against

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
#SBATCH -A CTLS2017      # <-- Allocation name to charge job against

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

Then look at the output when it finishes.

```
less host_dist*.o
```

You should see two distinct hostnames in your output.

You are now ready to utilize multiple nodes for your work at TACC. Launcher makes it that easy.

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
