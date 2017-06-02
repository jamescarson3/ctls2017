~~~ python
import random ,os
import multiprocessing

def list_append(count, out_list):
    # Appends a random number to the list ’count’ number of times. 
    # A CPU-heavy operation!
    print os.getpid(),’is working’
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

    print "List processing complete."
 ~~~
