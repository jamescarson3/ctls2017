# Python - Command-Line Programs - Argparse

## Questions

- How can I write Python programs that will work like more advanced Unix command-line tools more easily?

## Objectives

- Instead of handling `sys.argv` directly, use Python's `argparse` library.

As a command-line program increases in complexity past accepting a few positional arguments to adding optional arguments/flags, it makes sense to use `argparse`, the recommended command-line parsing module in the Python standard library.

### A minimal program

In the text editor of your choice, save the following code in a text file called, `parse.py`:

~~~python
import argparse
parser = argparse.ArgumentParser()
parser.parse_args()
~~~

Running the program a couple of times we observe several things:

~~~bash
$ python parse.py
$ python parse.py --help
usage: parse.py [-h]

optional arguments:
  -h, --help  show this help message and exit
$ python parse.py xxx
usage: parse.py [-h]
parse.py: error: unrecognized arguments: xxx
$ python parse.py -v
usage: parse.py [-h]
parse.py: error: unrecognized arguments: -v
~~~


- With no arguments or options, the program produces nothing.
- `--help` or `-h` produces a help message (for free!)
- The program recognizes and produces an error message for unknown arguments or options

### Positional arguments

OK, this program is not very useful right now. Let's add a positional argument using the `add_argument` method.

~~~python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("echo", help="echo back the string argument used")
args = parser.parse_args()
print("Echo:", args.echo)
~~~

While adding the `echo` positional argument, we also added a description of the argument that will show up in the auto-generated help message. Notice that we're also now getting back the argument values from the `parse_args` method. Let's try running this version of the program:

~~~bash
$ python parse.py
usage: parse.py [-h] echo
parse.py: error: the following arguments are required: echo
$ python parse.py -h
usage: parse.py [-h] echo

positional arguments:
  echo        echo back the string argument used

optional arguments:
  -h, --help  show this help message and exit
$ python parse.py message
Echo: message
~~~

We can see that by adding a positional argument the program will now produce an error message when running it without any argument.

### Argument type

What if we wanted our argument to be a number that we doubled (to use a trivial example)? Could we use `argparse` to restrict the argument to integers? Yes! Let's modify our program again and change the argument to only accept integers and then have the program double that argument.

~~~python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("double", type=int, help="a number to be doubled")
args = parser.parse_args()
print(args.double * 2)
~~~

~~~bash
$ python parse.py --help
usage: parse.py [-h] double

positional arguments:
  double      a number to be doubled

optional arguments:
  -h, --help  show this help message and exit
$ python parse.py x
usage: parse.py [-h] double
parse.py: error: argument double: invalid int value: 'x'
$ python parse.py 5
10
~~~

Now that we've restricted the double argument to an integer we see that `argparse` produces an error message when entering a non-integer argument.

### Optional arguments (and flags)

Now that we have a pretty good handle on positional arguments, let's try adding an optional argument (or two).

~~~python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("number", type=int, help="a number to be multiplied")
parser.add_argument("-m", "--multiply", type=int, default=2, help="multiply number by this")
parser.add_argument("-v", "--verbose", action="store_true", help="verbose output")
args = parser.parse_args()
if args.verbose:
    print("%i X %i = %i" % (args.number, args.multiply, args.number*args.multiply))
else:
    print(args.number * args.multiply)
~~~

Let's try running this program a couple of times:

~~~bash
$ python parse.py --help
usage: parse.py [-h] [-m MULTIPLY] [-v] number

positional arguments:
  number                a number to be multiplied

optional arguments:
  -h, --help            show this help message and exit
  -m MULTIPLY, --multiply MULTIPLY
                        multiply number by this
  -v, --verbose         verbose output
$ python parse.py 5
10
$ python parse.py --multiply 3 5
15
$ python parse.py 5 --multiply 3
15
$ python parse.py --verbose 5
5 X 2 = 10
$ python parse.py -v -m 4 5
5 X 4 = 20
~~~

We threw in a bunch of new parameters to the `add_argument` method. Let's digest them.

- a `-` or `--` added to the argument name turns it into an optional argument
- optional arguments can have more than one option string (in this example we used Unix short options)
- the `default=` parameter allows you to specify a default value if the option is not specified
- the verbose option is treated as a flag (True/False) by setting the `action=` parameter to `store_true`
- the order of the positional and optional arguments doesn't matter

### Conflicting options

In some cases, you might have options that don't work together or only one of several options can be chosen. The `argparse` library can handle this situation as well. Let's modify our previous example:

~~~python
import argparse

parser = argparse.ArgumentParser()
group = parser.add_mutually_exclusive_group()
group.add_argument("-v", "--verbose", action="store_true", help="verbose output")
group.add_argument("-q", "--quiet", action="store_true", help="quiet output")
parser.add_argument("number", type=int, help="a number to be multiplied")
parser.add_argument("-m", "--multiply", type=int, default=2, help="multiply number by this")
args = parser.parse_args()
answer = args.number * args.multiply

if args.quiet:
    print(answer)
elif args.verbose:
    print("%i multiplied by %i is equal to %i" % (args.number, args.multiply, answer))
else:
    print("%i X %i = %i" % (args.number, args.multiply, answer))
~~~

> #### Require one of option group
> Note that if you want to force one of the options in a mutually exclusive group to be specified, make it
> required.
> ~~~python
> group = parser.add_mutually_exclusive_group(required=True)
> ~~~

Let's run this modified program a couple of times:


~~~bash
$ python parse.py --help
usage: parse.py [-h] [-v | -q] [-m MULTIPLY] number

positional arguments:
  number                a number to be multiplied

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         verbose output
  -q, --quiet           quiet output
  -m MULTIPLY, --multiply MULTIPLY
                        multiply number by this
$ python parse.py 5
5 X 2 = 10
$ python parse.py -v -q 5
usage: parse.py [-h] [-v | -q] [-m MULTIPLY] number
parse.py: error: argument -q/--quiet: not allowed with argument -v/--verbose
$ python parse.py -v 5
5 multiplied by 2 is equal to 10
$ python parse.py -q 5
10
~~~

We can see that `argparse` will produce an error if both options are specified.

> ### Lots more
> There are a lot more ways to configure `argparse` and handle more complex options. For more information, please visit the [argparse reference](https://docs.python.org/3/library/argparse.html) that is part of Python's official documentation.

> ## Exercise
> In the previous [lesson](intro_to_python_100_cmdline.md) command-line programs were built by handling `sys.argv`
> and using `if/else` statements to handle any options. Modify the following program to use `argparse`:
>
> ~~~python
> import sys
> import numpy
>
> def main():
>     script = sys.argv[0]
>     action = sys.argv[1]
>     filenames = sys.argv[2:]
>     assert action in ['--min', '--mean', '--max'], \
>            'Action is not one of --min, --mean, or --max: ' + action
>     for f in filenames:
>         process(f, action)
>
> def process(filename, action):
>     data = numpy.loadtxt(filename, delimiter=',')
>
>     if action == '--min':
>         values = numpy.min(data, axis=1)
>     elif action == '--mean':
>         values = numpy.mean(data, axis=1)
>     elif action == '--max':
>         values = numpy.max(data, axis=1)
>
>     for m in values:
>         print(m)
>
> if __name__ == '__main__':
>    main()
> ~~~
>
> For this exercise, the program only needs to accept one file.
>
> **Bonus**: Read the [argparse reference](https://docs.python.org/3/library/argparse.html) and see if you
> can figure out how to accept multiple files.
>
> > ## Solution
> > ~~~python
> > import argparse
> > import numpy
> >
> > def main():
> >     parser = argparse.ArgumentParser()
> >     group = parser.add_mutually_exclusive_group(required=True)
> >     group.add_argument("--min", action="store_true", help="calculate the minimum")
> >     group.add_argument("--max", action="store_true", help="calculate the maximum")
> >     group.add_argument("--mean", action="store_true", help="calculate the mean")
> >     parser.add_argument("file", help="file to be processed")
> >     args = parser.parse_args()
> >     process(args)
> >
> > def process(args):
> >     data = numpy.loadtxt(args.file, delimiter=',')
> >
> >     if args.min:
> >         values = numpy.min(data, axis=1)
> >     elif args.mean:
> >         values = numpy.mean(data, axis=1)
> >     elif args.max:
> >         values = numpy.max(data, axis=1)
> >
> >     for m in values:
> >         print(m)
> >
> > if __name__ == '__main__':
> >    main()
> > ~~~
> {: .solution}

Previous: [Python - Command-Line Programs](intro_to_python_100_cmdline.md) | Top: [Python Overview](intro_to_python.md) | Next: [Python - Multiprocessing](intro_to_python_110_multiprocessing.md)
