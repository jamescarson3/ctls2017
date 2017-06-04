# Monitoring Jobs

Being able to accurately monitor a job is an invaluable skill.
It will enable you to measure how fast your analyses run, and help track down bugs when issues arise (they often do).

### Record Runtime

Whenever you run a large task, or want to compare the runtime of programs, the `time` command provides an easy way to track the runtime.
Lets give it a try.

```
$ time ls
```

After listing all of your directories, you should see some text that looks like this.

```
real    0m0.006s
user    0m0.000s
sys     0m0.000s
```

Where these values mean

| Row | Definition |
|-----|------------|
| real | Elapsed walltime |
| user | Time spent in user mode |
| sys | Time spend in kernel mode |

The real time will be the most important for us.
Now that we know how to interpret it, lets try running a longer task.

```
$ time sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head
```

Lets try again using our `LC_ALL=C` trick.

```
$ time LC_ALL=C sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head
```

By default, time prints

```
"real %f\nuser %f\nsys %f\n"
```

but we can also print verbose statistics by calling it directly with the `-v` argument

```
$ LC_ALL=C /usr/bin/time -v sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head
```

#### Explore

- Try timing some other commands you know

### Interactive Monitoring

Sometimes you run a longer pipeline with multiple programs and you want to see how each process is running instead of summary statistics at the end.
The `top` program is a good way to monitor **currently** running tasks.

Lets monitor our un-optimized sort and see what it looks like.
First, we are going to launch it as a background process with the `&` character, and then immediately monitor it with top before it exits.

```
$ sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head &
$ top
```

After `sort` finishes, quit top the same way you quit `less` - by hitting `Q`.

If all the root processes are confusing to you, you can decide to only show your processes by launching it with the `-u` argument.

```
$ sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head &
$ top -u [username]
```

While inside top, you can also sort by

- Memory (`f` then `n` then `Enter`)
- CPU (`f` then `k` then `Enter`)
- PID (`f` then `a` then `Enter`)

I recommend using top to monitor the following things when using a tool for the first time:

- How many cores does it use?
  - Each 100% corresponds to a core or thread
- How many programs run at the same time?
  - Watch to make sure you are not over saturating the node with processes
- How much memory is being used?
  - When a program fails, I will often watch it to make sure it never gets close to 100% memory usage.

#### Explore

- Try monitoring other commands you know

### Passive monitoring

For times when you job is too long to watch with `top` and the summary satistics provided by `time` are insufficient, [REMORA](https://github.com/TACC/remora) is a powerful and easy to use tool.
REMORA was developed at TACC, so we deploy it on each system, but it can also be installed on any other system.
After loading the `remora` module, you use it the same way you use time. All performance metrics are recorded to files for you to view after your run.
Lets give it a try using our `sort` example.

```
$ module load remora
$ remora sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head
```

Performance statistics are recorded every 10 seconds by default, and those metrics can be found int the `remora_[jobid]` folder that is created.

```
$ nid01040(32)$ head remora_867614/CPU/cpu_nid01040.txt                                               
 %time 1496537190                                                                                   
 %usr 1.99 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 95.96 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00                                                 
 %sys 0.08 1.00 0.00 0.99 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 3.03 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00                                                  
 %idle 97.92 99.00 100.00 99.01 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 1.01 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00                                                        
 %time 1496537200                                                                                   
 %usr 2.10 0.00 0.00 0.00 100.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00                                                
 %sys 0.02 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00                                                  
 %idle 97.88 100.00 100.00 100.00 0.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00 100.00                                                      
 %time 1496537211                                                                                   
 %usr 2.08 0.00 0.00 0.00 100.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00 0.00    
```                                            

You can also generate figures using the `remora_post` command.

```
$ module load python
$ remora_post
```

Which generates PNG files you can download and view.

#### Explore

- Try monitoring other commands you know
<br>
<br>

[Back - Introduction](optimization_parallelization_01.md)
&nbsp;&nbsp;&#151;&nbsp;&nbsp;
[Next - Parallelization](optimization_parallelization_03.md)
