# Python - Hands On Topics

---

## Installing Python Modules

Follow along with [this static notebook](python_modules.html) to learn how to install non-standard python packages. Remember for for Lonestar 5, you need to do the following:
~~~python
module load python
pip --trusted-host pypi.python.org install --user moduleyouneed
~~~

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

## Faster!
Try making **multi_process.py** run even faster.  Use any technique, but the same 400,000,000 multiplications must be calculated.  

---

## Biopython
Explore the [Biopython Tutorial and Cookbook](http://biopython.org/DIST/docs/tutorial/Tutorial.html).  Many functions have been created to assist with common life science computing tasks.  See anything that could help you?

---

Previous: [Python - Multiprocessing](intro_to_python_110_multiprocessing.md) | Top: [Python Overview](intro_to_python.md)
