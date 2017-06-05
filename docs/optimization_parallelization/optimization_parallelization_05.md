# Code Optimization

Whenever you write a program in non-interprative languages like C, C++, or Fortran, it gets converted into machine code that the processor understands.
Our machines specifically understand x86_64.
Other chips like those in your phones understand ARM (RISC) code.

If you have ever taken a programming class and had to write algorithms to print out Fibonacci numbers, you know probably know there are many ways to achieve the same result.
Some of those ways are also faster than others.
The same rules apply to the code that assemblers generate.

At TACC, whenever we deploy software, we experiment with different ways to compile code.
We know these tools will be used by researchers around the world, and we want to make sure the software not only works, but runs as quickly as possible.
We are going to experiment with the program [FLASh](https://ccb.jhu.edu/software/FLASH/) today and learn some tricks to optimize code.

### Default

When you copied over the data files, you already copied over the FLASH source code, so let's try compiling it and running it.

First, compile it using default parameters using the GCC compiler. Notice we will be running all of this from `/dev/shm` so no slowdowns are introduced by the network filesystems. Just like on your home wifi, someone might be streaming ALL of youtube.

```
$ cp SRR*fastq /dev/shm
$ cd /dev/shm
$ tar -xzf ~/FLASH-1.2.11.tar.gz
$ cd FLASH-1.2.11
$ module load gcc
$ make CC=gcc
```

Now, we can run it.

```
$ ./flash -m 20 -M 250 -t 1 ../SRR2014925_1.fastq ../SRR2014925_2.fastq
```

Conveniently, FLASH provides a runtime at the end, so we can compare all of our runtimes for different ways to compile.
Lets also run it one more time, but record the output to a log file.

```
$ ./flash -m 20 -M 250 -t 1 ../SRR2014925_1.fastq ../SRR2014925_2.fastq &> default.log
```

### Optimization Level

By default, FLASh compiles with an optimization level of 2 (`-O2`).
Lets see what happens with an optimization level of 3, which is also the maximum.

```
$ make clean
$ make CC=gcc CFLAGS="-O3 -Wall -std=c99 -D_GNU_SOURCE -D_FILE_OFFSET_BITS=64"
```

After compiling, we should test again.

```
$ ./flash -m 20 -M 250 -t 1 ../SRR2014925_1.fastq ../SRR2014925_2.fastq &> O3.log
$ tail O3.log
```

Was there a speedup?

```
Speedup = Default/O3
```

### Auto-vectorization

We can also specify the architecture of our CPU to allow the compiler the chance to auto-vectorize some loops.
This means that several operations can take place during each clock cycle.
[Lonestar 5](https://portal.tacc.utexas.edu/user-guides/lonestar5#architecture-computenodes) compute nodes use Intel Haswell processors, so we can specifically target them with the `-march=haswell` flag.

```
$ make clean
$ make CC=gcc CFLAGS="-O3 -march=haswell -Wall -std=c99 -D_GNU_SOURCE -D_FILE_OFFSET_BITS=64"
$ ./flash -m 20 -M 250 -t 1 ../SRR2014925_1.fastq ../SRR2014925_2.fastq &> avx2.log
$ tail avx2.log
```

For times when you do not know the exact architecture, you can use `-march=native`. Just remember that this binary may not work on another system.

### Thread Scaling

Now that we have an optimal sequential version of our code, lets try running it with different core counts and see how well it scales.

```
$ for N in {1..24}
$ do
$   ./flash -m 20 -M 250 -t $N ../SRR2014925_1.fastq ../SRR2014925_2.fastq &> avx2_${N}.log
$ done
```

#### Explore

- Try plotting your runtimes
- Do you see an obvious slowdown?

## Exercises

- Optimize a tool that you use
<br>
<br>

[Back - Task Distribution](optimization_parallelization_04.md)
&nbsp;&nbsp;&#151;&nbsp;&nbsp;
[Next - Hardware](optimization_parallelization_06.md)