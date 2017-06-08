# Multiprocessing with Python

**Objectives**
 - Learn how to distribute work in python over multiple processors using the **multiprocessing** library

**Assumptions**
- Familiarity with the concept of multiprocessing.
- Basic knowledge of linux commands, text editing, and accessing TACC systems
- Active allocation on ls5.tacc.utexas.edu

---

There are several different python libraries for performing multiple tasks simultaneously.  This lesson introduces the multiprocessing library, which can be a useful approach for leveraging the power of multicore nodes on an HPC system.

Generally, a python script will execute on only one core.  A node on Lonestar 5 has 24 cores, therefore a typical python script is using only a small fraction of the potential computing power available on a node.  Depending on the task, you may be able to use more of the nodes power, reducing the time required to complete the job.

There are **four** changes to add to a python script to utilize **multiprocessing**.
1. Import the **multiprocessing** library
2. Use **multiprocessing.Process** to define which function goes to its own processing core
3. Initiate the processes using **start**.
4. Note when all processes have finished using **join** so that the python script can continue.

---

Let us start with an example python script that does a lot of math without multiprocessing.

Log into Lonestar 5 and add this script to your directory there.

~~~ python
# one_process.py
import time

op_count = 400000000    # number of operations to perform

def lots_of_math(N1,N2):
    for n in range(N1,N2):
        m=n*n

tt = time.time()        # start recording time

lots_of_math(0,op_count)

print("done in : "+str(time.time()-tt))	    # report elapsed time
~~~

Now go ahead and grab your own node using idev, load the python3 module (gcc is pre-requisite), and try running the program.

~~~ bash
idev
module load gcc/4.9.3
module load python3/3.5.2
python3 one_process.py
~~~

How long did the program take to run?

Run the program again, this time in the background and use **top** to see how much of the node's processing power is being used.

~~~ bash
python3 one_process.py &
top
~~~

---

Now let us add **multiprocessing** to the program to hopefully make it twice as fast by dividing the workload between two processes.  The four changes to make are noted in the script below.  Add this script to your directory on Lonestar5.

~~~ python
# two_process.py
import time
import multiprocessing      # CHANGE 1 - import the multiprocessing library

op_count = 400000000    # number of operations to perform

def lots_of_math(N1,N2):
    for n in range(N1,N2):
        m=n*n

tt = time.time()        # start recording time

# CHANGE 2 - assign processes
half_count = int( op_count / 2 )
t1 = multiprocessing.Process(target=lots_of_math, args=(0,half_count))
t2 = multiprocessing.Process(target=lots_of_math, args=(half_count,op_count))

# CHANGE 3 - initiate processes
t1.start()
t2.start()

# CHANGE 4 - wait until all processes finish before moving on
t1.join()
t2.join()

print("done in : "+str(time.time()-tt))	    # report elapsed time
~~~

Now let's run it and see how long it takes.

~~~ bash
python3 two_process.py
~~~

Is it twice as fast?

Let us run it in the background and see how much of the node's processing power is being used now.

~~~ bash
python3 two_process.py &
top
~~~

What differences do you see in top between using one process and two processes?

---

Doubling your speed is nice, but wouldn't you sleep better at night knowing that your submitted job is optimally utilizing the node?

However, adding three lines of code for every additional process used may not be what you want to do.  A solution is to create a list of processes.

Here the script has been modified to work on an arbitrary number of processes, based on user input.

~~~ python
# multi_process.py
import time
import multiprocessing

proc_count = int(input ("Enter number of processes: "))   # number of processes to create

op_count = 400000000    # number of operations to perform

def lots_of_math(N1,N2):
    for n in range(N1,N2):
        m=n*n

tt = time.time()        # start recording time

op_proc = int( op_count / proc_count )	# number of operations per process
P = []					# initialize list of processes

for i in range(proc_count):
    P.append( multiprocessing.Process( target=lots_of_math, args=(i*op_proc, (i+1)*op_proc) ) )

for i in range(proc_count):
    P[i].start()

for i in range(proc_count):
    P[i].join()

print("done in : "+str(time.time()-tt))	    # report elapsed time
~~~

Run it using the following command.

~~~ bash
python3 multi_process.py
~~~

What number of processes on Lonestar5 completes the quickest on a single node?

---

There is an even more automated approach for splitting up work across nodes: **map and pool**.

~~~ python
# map_pool.py
import time
import multiprocessing

proc_count = int(input ("Enter number of processes: "))   # number of processes to create

op_count = 40000000    # number of operations to perform

def lots_of_math(n):
    m=n*n    

tt = time.time()        # start recording time

p = multiprocessing.Pool(processes=proc_count)

p.map(lots_of_math,(range(0,op_count)))
p.close()
p.join()

print("done in : "+str(time.time()-tt))	    # report elapsed time
~~~

Note that I decreased the number of operations by a factor of 10.  
Often map & pool can lead to faster solutions.  
Why was it slower in this example?  


Previous: [Python - Command-Line Programs - Argparse](intro_to_python_101_argparse.md) | Top: [Python Overview](intro_to_python.md) | Next: [Python - Exercises](intro_to_python_500_exercises.md)
