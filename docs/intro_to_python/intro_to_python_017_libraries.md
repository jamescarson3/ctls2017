# Python - Numpy and Arrays

### Objectives:
- Explain what a library is, and what libraries are used for.
- Import a Python library and use the functions it contains.
- Read tabular data from a file into a program.
- Perform operations on arrays of data.

---
Words are useful, but what's more useful are the sentences and stories we build with them.
Similarly, while a lot of powerful, general tools are built into languages like Python,
specialized tools built up from these basic units live in [libraries](python_reference.md#library) 
that can be called upon when needed.

In order to load our inflammation data, we need to [import](python_reference.md#import) (that is, access)
a library called [NumPy](http://docs.scipy.org/doc/numpy/ "NumPy Documentation").
In general, you should use this library if you want to do fancy things with numbers,
especially if you have matrices or arrays. We can import NumPy using:

~~~ python
import numpy
~~~

Importing a library is like getting a piece of lab equipment out of a storage locker and setting it up on the bench.
Libraries provide additional functionality to the basic Python package,
much like a new piece of equipment adds functionality to a lab space. Just like in the lab, importing too many libraries
can sometimes complicate and slow down your programs - so we only import what we need for each program.

Once you've imported the NumPy library, we can ask the library to read our data file for us.

> ### Copying the data file
>
> Before reading the data file, we need a local copy of the file.
> We can access many linux commands using the **system** function of the **os** library.
> Here, we will use the **wget** command.
>
> ~~~ python
> import os
> os.system('wget https://raw.githubusercontent.com/swcarpentry/python-novice-inflammation/gh-pages/data/inflammation-01.csv')
> ~~~
>

Ok, *now* we can use NumPy to read the data file.

~~~ python
numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
~~~

The expression `numpy.loadtxt(...)` is a [function call](python_reference.md#function)
that asks Python to run the [function](python_reference.md#function) `loadtxt` which belongs to the `numpy` library.
This dotted notation is used everywhere in Python
to refer to the parts of things as `thing.component`.

`numpy.loadtxt` has two [parameters](python_reference.md#parameter):
the name of the file we want to read,
and the [delimiter](python_reference.md#delimiter) that separates values on a line.
These both need to be character [strings](python_reference.md#string),
so we put them in quotes.

Since we haven't told it to do anything else with the function's output,
the notebook displays it.
In this case, that output is the data we just loaded.
By default, only a few rows and columns are shown
(with `...` to omit elements when displaying big arrays).
To save space, Python displays numbers as `1.` instead of `1.0`
when there's nothing interesting after the decimal point.

Our call to `numpy.loadtxt` read our file, but didn't save the data in memory.
To do that, we need to assign the array to a variable. 
Just as we can assign a single value to a variable, we can also assign an array of values
to a variable using the same syntax.  Let's re-run `numpy.loadtxt` and save its result:

~~~ python
data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
~~~

This statement doesn't produce any output because assignment doesn't display anything.
If we want to check that our data has been loaded,
we can print the variable's value:

~~~ python
print(data)
~~~

Now that our data is in memory, we can start doing things with it.
First, let's ask what [type](python_reference.md#type) of thing `data` refers to:

~~~ python
print(type(data))
~~~

The output tells us that `data` currently refers to
an N-dimensional array created by the NumPy library.
These data correspond to arthritis patients' inflammation.
The rows are the individual patients and the columns
are their daily inflammation measurements.

> ### Data Type
>
> A Numpy array contains one or more elements
> of the same type. `type` will only tell you that
> a variable is a NumPy array.
> We can also find out the type
> of the data contained in the NumPy array.
>
> ~~~ python
> print(data.dtype)
> ~~~
>
> This tells us that the NumPy array's elements are
> **floating-point numbers**.

We can see what the array's [shape](python_reference.md#shape) is like this:

~~~ python
print(data.shape)
~~~

This tells us that `data` has 60 rows and 40 columns. When we created the
variable `data` to store our arthritis data, we didn't just create the array, we also
created information about the array, called [members](python_reference.md#member) or
attributes. This extra information describes `data` in
the same way an adjective describes a noun.
`data.shape` is an attribute  of `data` which describes the dimensions of `data`.
We use the same dotted notation for the attributes of variables
that we use for the functions in libraries
because they have the same part-and-whole relationship.

If we want to get a single number from the array,
we must provide an **index** in square brackets,
just as we do in math:

~~~ python
print('first value in data:', data[0, 0])
~~~

~~~ python
print('middle value in data:', data[30, 20])
~~~

The expression `data[30, 20]` may not surprise you, but `data[0, 0]` might.
Programming languages like Fortran, MATLAB and R start counting at 1,
because that's what human beings have done for thousands of years.
Languages in the C family (including C++, Java, Perl, and Python) count from 0
because it represents an offset from the first value in the array (the second
value is offset by one index from the first value). This is closer to the way
that computers represent arrays.

As a result, if we have an M×N array in Python,
its indices go from 0 to M-1 on the first axis
and 0 to N-1 on the second. It takes a bit of getting used to,
but one way to remember the rule is that
the index is how many steps we have to take from the start to get the item we want.

> ### In the Corner
>
> What may also surprise you is that when Python displays an array,
> it shows the element with index `[0, 0]` in the upper left corner
> rather than the lower left.
> This is consistent with the way mathematicians draw matrices,
> but different from the Cartesian coordinates.
> The indices are (row, column) instead of (column, row) for the same reason,
> which can be confusing when plotting data.

An index like `[30, 20]` selects a single element of an array,
but we can select whole sections as well.
For example,
we can select the first ten days (columns) of values
for the first four patients (rows) like this:

~~~ python
print(data[0:4, 0:10])
~~~

The [slice](python_reference.md#slice) `0:4` means,
"Start at index 0 and go up to, but not including, index 4."
Again, the up-to-but-not-including takes a bit of getting used to,
but the rule is that the difference between the upper and lower bounds is the number of values in the slice.

We don't have to start slices at 0:

~~~ python
print(data[5:10, 0:10])
~~~

We also don't have to include the upper and lower bound on the slice.
If we don't include the lower bound, Python uses 0 by default;
if we don't include the upper, the slice runs to the end of the axis,
and if we don't include either (i.e., if we just use ':' on its own),
the slice includes everything:

~~~ python
small = data[:3, 36:]
print('small is:')
print(small)
~~~

> ### Exercise
> 
> Sometimes we want to refer to the last value or values in an array, without knowing the array size.
> Any ideas on how to do this?  
>
> Try to slice the value of the last row and last column of `data`.
>
> > ### Solution
> > ~~~python
> > print( data[-1, -1] )
> > ~~~
> {: .solution}



Arrays also know how to perform common mathematical operations on their values.
The simplest operations with data are arithmetic:
add, subtract, multiply, and divide.
 When you do such operations on arrays,
the operation is done on each individual element of the array.
Thus:

~~~
doubledata = data * 2.0
~~~

will create a new array `doubledata`
whose elements have the value of two times the value of the corresponding elements in `data`:

~~~
print('original:')
print(data[:3, 36:])
print('doubledata:')
print(doubledata[:3, 36:])
~~~

If,
instead of taking an array and doing arithmetic with a single value (as above)
you did the arithmetic operation with another array of the same shape,
the operation will be done on corresponding elements of the two arrays.
Thus:

~~~
tripledata = doubledata + data
~~~

will give you an array where `tripledata[0,0]` will equal `doubledata[0,0]` plus `data[0,0]`,
and so on for all other elements of the arrays.

~~~
print('tripledata:')
print(tripledata[:3, 36:])
~~~

**Keypoints:**
- Import a library into a program using `import libraryname`.
- Use the `numpy` library to work with arrays in Python.
- The expression `array.shape` gives the shape of an array.
- Use `array[x, y]` to select a single element from an array.
- Array indices start at 0, not 1.
- Use `low:high` to specify a slice that includes the indices from `low` to `high-1`.
- All the indexing and slicing that works on arrays also works on strings.

---

Previous: [Python - Variables & Memory](intro_to_python_016_variables.md) | Top: [Python Overview](intro_to_python.md) | Next: [Python - Functions & Plotting](intro_to_python_018_plotting.md)
