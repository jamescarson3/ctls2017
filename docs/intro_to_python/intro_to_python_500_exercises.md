# Python - Hands On Topics

---

## Interacting with your Data
Python has several libraries for building Graphical User Interfaces, including [Tkinter](https://wiki.python.org/moin/TkInter) and [wxPython](https://wxpython.org/).  Jupyter also has ways to interact with the data, by using [Widgets](https://ipywidgets.readthedocs.io/en/latest/examples/Using%20Interact.html).  Working with the inflammation dataset, can you update the script to include a scroll bar that allows you to select which datasets are graphed?

> ## Solution
>
> First make sure you are in the directory with the data.
>
> ~~~python
> %matplotlib inline
> 
> import numpy
> import glob
> import matplotlib.pyplot
> from ipywidgets import interact
> 
> # make sure you are already in the directory with the data
> filenames = sorted(glob.glob('inflammation*.csv'))
> 
> # create a new list to hold all the data
> all_data=[]
> 
> # for each data file, append the contents to the data list
> for f in filenames:
>     print(f)
>     all_data.append(numpy.loadtxt(fname=f, delimiter=','))
> 
> # use widgets to select the array
> @interact(x=(0,11,1))
> def plot_mean_max_min(x=0):
>     fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))
> 
>     axes1 = fig.add_subplot(1, 3, 1)
>     axes2 = fig.add_subplot(1, 3, 2)
>     axes3 = fig.add_subplot(1, 3, 3)
> 
>     axes1.set_ylabel('average')
>     axes1.plot(numpy.mean(all_data[x], axis=0))
> 
>     axes2.set_ylabel('max')
>     axes2.plot(numpy.max(all_data[x], axis=0))
> 
>     axes3.set_ylabel('min')
>     axes3.plot(numpy.min(all_data[x], axis=0))
> 
>     fig.tight_layout()
>     matplotlib.pyplot.show()
> ~~~
{: .solution}

---

## *Pandas* - The Python Data Analysis Library
The Pandas library is an excellent option for working with tabular datasets.  If you plan to process and visualize data of this type using Python, it is a good idea to learn more about using Pandas.  Data Carpentry has an [excellent tutorial](http://www.datacarpentry.org/python-ecology-lesson/) on analysing tabular data, using an [ecology dataset](data/surveys.csv) as the example.   

---

## Threading

## Pool and map



## Viewing images through ssh

## Compiling python and/or Cython

## Biopython

Previous: [Python - Multiprocessing](intro_to_python_110_multiprocessing.md) | Top: [Python Overview](intro_to_python.md)
