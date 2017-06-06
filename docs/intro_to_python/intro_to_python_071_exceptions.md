# Python - Errors and Exceptions - Exception Handling

## Questions

- How can I raise exceptions in Python?
- How can I catch an exception?

## Objectives

- To be able to raise an exception.
- To be able to catch an exception using a `try/except` block.
- To understand the Python error class hierarchy.

## Raising Exceptions

We've seen that when Python encounters an error it throws an Exception. Depending on the error, a different type of Exception will be thrown. In fact, the programmer can throw an Exception at any time using the [raise](https://docs.python.org/3/reference/simple_stmts.html#raise) keyword.

~~~python
raise Exception('Error, yikes, time to get out!')
~~~

~~~
---------------------------------------------------------------------------
Exception                                 Traceback (most recent call last)
<ipython-input-89-1c2b167e2dc4> in <module>()
----> 1 raise Exception('Error, yikes, time to get out!')

Exception: Error, yikes, time to get out!
~~~

By default, exceptions will interrupt the execution of code and exit the program/script. But what if this is not what we want, can we 'handle' the exception? Yes!

## Catching Exceptions

Handling Exceptions is done by wrapping a block of code with a [try/except](https://docs.python.org/3/reference/compound_stmts.html#except) statement.

~~~python
try:
    file_handle = open('myfile.txt', 'r')
except FileNotFoundError:
    print('Error: file myfile.txt can not be found!')
~~~

~~~
Error: file myfile.txt can not be found!
~~~

Since the **try/except** statement can wrap more than one line of code, it can also have multiple except clauses to handle different potential exceptions. In the following code, we can see that there are at least two places which might throw exceptions; trying to open a file that may or may not exist and the conversion of numbers read from a file to integers. Here is what the file **bad-small-02.csv** contains:

~~~
9,17,15,x
20,8,5
~~~

*Note that the except clauses should be ordered from the specific to the more general as the first (and only) exception that matches will be thrown.*

~~~python
try:
    file_handle = open('bad-small-02.csv', 'r')
    line = file_handle.readline().rstrip()
    values = line.split(',')
    mysum = 0
    for value in values:
        mysum += int(value.strip())
    print(mysum)
except FileNotFoundError as fe:
    print('Error: %s' % fe)
except ValueError as ve:
    print('Error: line contains non-integer value (%s)' % ve)
except:
    print('Unknown error')
    raise
~~~

~~~
Error: line contains non-integer value (invalid literal for int() with base 10: 'x')
~~~

But what if we don't know what exception is potentially going to be thrown. Since Python is an object-oriented language, exceptions are classes and have a class hierarchy ([Python3](https://docs.python.org/3/library/exceptions.html#exception-hierarchy) / [Python2](https://docs.python.org/2/library/exceptions.html#exception-hierarchy)). We can always catch a more general exception. Here is a look at the top of the Python3 exception hierarchy:

~~~
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- StopAsyncIteration
      +-- ArithmeticError
      |    +-- FloatingPointError
      |    +-- OverflowError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- BufferError
      +-- EOFError
      +-- ImportError
           +-- ModuleNotFoundError
      +-- LookupError
      |    +-- IndexError
      |    +-- KeyError
      +-- MemoryError
      +-- NameError
      |    +-- UnboundLocalError
      +-- OSError
      |    +-- BlockingIOError
      |    +-- ChildProcessError
      |    +-- ConnectionError
      |    |    +-- BrokenPipeError
      |    |    +-- ConnectionAbortedError
      |    |    +-- ConnectionRefusedError
      |    |    +-- ConnectionResetError
      |    +-- FileExistsError
      |    +-- FileNotFoundError
      |    +-- InterruptedError
      |    +-- IsADirectoryError
      |    +-- NotADirectoryError
      |    +-- PermissionError
      |    +-- ProcessLookupError
      |    +-- TimeoutError
~~~

We can see that lots of errors fall under **Exception**. Let's rewrite the above section of code with just a single except clause. In this case, we're just printing out the message given by the thrown exception.

~~~python
try:
    file_handle = open('bad-small-02.csv', 'r')
    line = file_handle.readline().rstrip()
    values = line.split(',')
    mysum = 0
    for value in values:
        mysum += int(value.strip())
    print(mysum)
except Exception as e:
    if hasattr(e, 'message'):
        print('Error: %s' % e.message)
    else:
        print('Error: %s' % e)
~~~

~~~
Error: invalid literal for int() with base 10: 'x'
~~~

So far, the examples have basically caught the exceptions to show a more nicely formatted error message (and avoid showing the traceback). While tracebacks are good for the developer, it is arguably better to not show them to end users. Can we do more with the caught exception? In some cases, it may be possible to *fix* the error in the except clause and continue running the code. Here is a (completely contrived) example:

~~~python
var1 = '1'
try:
    var2 = var1 + 1  # since var1 is a string it cannot be added to the number 1
except:
    print('Converting var1 to integer...')
    var2 = int(var1) + 1
print('Total:', var2)
~~~

~~~
Converting var1 to integer...
Total: 2
~~~

Previous: [Python - Errors and Exceptions](intro_to_python_070_errors.md) | Top: [Python Overview](intro_to_python.md) | Next: [Python - Defensive Programming](intro_to_python_080_defensive.md)
