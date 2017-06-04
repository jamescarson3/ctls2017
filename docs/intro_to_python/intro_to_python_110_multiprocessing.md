# Multiprocessing with Python

### Objectives
 - Learn how to distribute work in python over multiple processors using the **multiprocessing** library
 
### Assumptions
- Familiarity with the concept of multiprocessing.
- Basic knowledge of linux commands, text editing, and accessing TACC systems
- Active allocation on ls5.tacc.utexas.edu

There are several different python libraries for performing multiple tasks simultaneously.  This lesson introduces the multiprocessing library, which can be a useful approach for leveraging the power of multicore nodes on an HPC system.

Generally, a python script will execute on only one core.  A node on Lonestar 5 has 24 cores, therefore a typical python script is using only a small fraction of the potential computing power available on a node.  Depending on the task, you may be able to use more of the nodes power, reducing the time required to complete the job.

There are **four** changes to add to a python script to utilize **multiprocessing**.
1. Import the **multiprocessing** library
2. Use **multiprocessing.Process** to define which function goes to its own processing core
3. Initiate the processes using **start**.
4. Note when all processes have finished using **join** so that the python script can continue.

Example - Without multiprocessing

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

~~~ bash
idev
module load gcc/4.9.3
module load python3/3.5.2
python3 one_process.py
~~~

~~~
python3 one_process.py &
top
~~~


Example - Two processes

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





~~~
t=[]
for i in range(number_of_threads):
    t.append( multiprocessing.Process(target=lots_of_math, args=(i, number_of_operations_per_thread)) )
    
for i in range(number_of_threads):
    t[i].start()
    #print(i,"started")
    
for i in range(number_of_threads): 
    t[i].join()
    #print(i,"joined")
	
print("done in : "+str(time.time()-tt))	
~~~


Example - add in multiprocessing with 2 cores

Example - variable number of cores



To begin, log in to ls5.tacc.utexas.edu from your terminal.

Create the following file:

~~~ python
import time
import multiprocessing

number_of_threads = 10 #int(input ("Enter number of threads: "))
number_of_operations = 10000000000
number_of_operations_per_thread = int( number_of_operations / number_of_threads )

def lots_of_math(thread_number, operation_count):
    x1=thread_number*operation_count
    x2=x1+operation_count
    m=0
    for n in range(x1,x2):
        m=n*n
    #print(thread_number,"finished",x1,x2,m)
	
tt = time.time()

t=[]
for i in range(number_of_threads):
    t.append( multiprocessing.Process(target=lots_of_math, args=(i, number_of_operations_per_thread)) )
    
for i in range(number_of_threads):
    t[i].start()
    #print(i,"started")
    
for i in range(number_of_threads): 
    t[i].join()
    #print(i,"joined")
	
print("done in : "+str(time.time()-tt))	
~~~



~~~ python
import random ,os
import multiprocessing

def list_append(count, out_list):
    # Appends a random number to the list ’count’ number of times. 
    # A CPU-heavy operation!
    print(os.getpid(),"is working")
    for i in range(count):
        out_list.append(random.random())

    if __name__ == "__main__":
        size = 10000000 # Number of random numbers to add
        procs = 2 # Number of processes to create

        # Create a list of processes and define work for each process
        process_list = []

    for i in range(0, procs):
        out_list = list()
        process = multiprocessing.Process(target=list_append, args=(size, out_list))
        process_list.append(process)

    # Start the processes (i.e. calculate the random number lists)
    for p in process_list:
        p.start()

    # End all of the processes have finished
    for p in process_list:
        p.join()

    print("List processing complete.")
 ~~~
