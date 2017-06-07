# Parallelizing Jobs

According to the [Stanford CPU database](http://cpudb.stanford.edu/), processors haven't gotten faster since 2005.

![clock rates](https://github.com/CODE-at-TACC/summer-2015/raw/master/parallel/images/clock.png)

No matter how much we've spent on the latest and greatest PC, sequential (single-core) programs won't be going any faster. Even at TACC, Stampede processors ran between 2.7 and 3.5 GHz and Stampede 2 processors run at 1.4 GHz.

However, transistor and core counts are increasing.

![transistors](https://github.com/CODE-at-TACC/summer-2015/raw/master/parallel/images/transistors.png)

Stampede had 16 cores in the main CPU, while Stampede 2 will have 68! We can take advantage of these resources with threaded code and concurrent task scheduling.

### Threaded Applications

The most proactive thing we can do is run our applications on multiple threads/processors when possible. This means reading the manual, finding the option for scaling execution, and usually setting it to correspond with the system core count.

| TACC System | Cores/Node |
|--|--|
| Stampede | 16 |
| Stampede 2 | 68 |
| Lonestar 5 | 24 |
| Maverick | 20 |
| Wrangler | 24 |

The version of `sort` on LS5 does have a parallel option, so lets give it a try using our standard workflow.

```
$ time sort -S 100M -k1,1 -k2,2n SRR2014925.bed | head
$ time sort --parallel 24 -S 100M -k1,1 -k2,2n SRR2014925.bed | head
```

We can also use a loop to see where increasing the number of threads becomes ineffective.

```
for N in {1..6}
do
   time sort --parallel $N -S 100M -k1,1 -k2,2n SRR2014925.bed > /dev/null
done 2>&1 | grep "real" | awk '{ print NR"\t"$0 }'
```

Time writes to `stderr` instead of `stdout`, so we need the `2>&1` redirection to grep for real time.

Do you see a point where extra cores becomes ineffective? Does increasing the memory limit help?

#### Explore

- Try experimenting with or reading about thread count on other tools you know
  - BWA
  - samtools
  - tophat
  - bowtie

### Concurrent Processes

When programs don't allow thread scaling, or they do not scale after a certain limit like `sort`, we have the option to run multiple programs at the same time - assuming there is leftover memory and i/o.
The most basic version of this is multitasking by running multiple programs in the background.
Starting from a sequential example

```
time for N in {1..4}
do
   sleep 2 && echo "$N - Done - $(date +%s)"
   sleep 1
done
```

The scheduling would look like this

```
N 123456789012
1 SSE
2    SSE
3       SSE
4          SSE
```

This should take about 3 seconds per loop, so hopefully 12 seconds in total. We can run multiple tasks in parallel by launching the sleep/echo line in the background and not waiting for it to complete.

```
time for N in {1..4}
do
   ( sleep 2 && echo "$N - Done - $(date +%s)" ) &
   sleep 1
done
```

The parallel scheduling would look like

```
N 12345
1 SE
2  SE
3   SE
4    SE
```

However, you may notice that time prints before the 4th task finishes.
That's because the for loop, and `time`, exits before the backgrounded task finishes.
We cane make this much more apparent with

```
time for N in {1..4}
do
   ( sleep 2 && echo "$N - Done - $(date +%s)" ) &
done
```

If we use `wait` at the end of our for loop, the program will block until all the child processes are completed.

```
time ( for N in {1..4}
do
   ( sleep 2 && echo "$N - Done - $(date +%s)" ) &
done && wait)
```

The parallel scheduling now looks like

```
N 12
1 SE
2 SE
3 SE
4 SE
```

And assuming we have at least 4 cores in our computer, this is what we want.
When you start writing workflows with large numbers of tasks, it becomes difficult to schedule everything programmatically, so I recommend the `xargs` command to work through everything for you.

```
time for N in {1..4}
do
   echo "sleep 2 && echo '$N - Done - $(date +%s)'"
done | xargs -L 1 -P 4 -I {} bash -c {}
```

When `xargs` recieves the `-L 1` argument, it will run an entire line (which we echo). The `-P` argument controls the number of cores you want to schedule the tasks on, and the `-I {}` argument will substitute the input line as `{}` at the end.

You can also send a list directly to xargs and specify that each word (`-n 1`) be executed on, making it trivial to compress

```
$ ls *fastq *fasta
$ ls *fastq *fasta | xargs -n 1 -P 24 gzip
$ ls *fastq* *fasta*
```

and decompress files.

```
$ ls *fastq* *fasta*
$ ls *fastq* *fasta* | xargs -n 1 -P 24 gzip -d
$ ls *fastq* *fasta*
```

#### Explore

- Use for/wait to calculate the line count of each fastq file
- Use `ls` and `xargs` to count fastq lines in parallel

## Exercises

- Use the `split` command to make a parallel merge-sort
<br>
<br>

[Back - Monitoring Jobs](optimization_parallelization_02.md)
&nbsp;&nbsp;&#151;&nbsp;&nbsp;
[Next - Task Distribution](optimization_parallelization_04.md)
