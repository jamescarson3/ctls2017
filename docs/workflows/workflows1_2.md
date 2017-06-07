# Life Sciences Workflows

## Automating workflows 1

While our app is running, let's start looking at what we will eventually want to do to make our lives easier when running blastp.  Let's write our own script to automate (and document) our process.

```
# are we in the right directory?
pwd

# create the script file and make it executable
touch blastp_workflow.sh
chmod +x blastp_workflow.sh

# now open this file in your favorite text editor
# e.g. "vim blastp_workflow.sh"
```

Our blastp_workflow.sh script can start out something like this:

```
#!/bin/bash

echo "workflow started at $(date)"

# validate and preprocess our input file(s)
query="first10.pep"
database="/work/01114/jfonner/public/ctls2017/refseq_protein/refseq_protein"

# run blastp
blastp -num_threads 12 -query $query -db $database

# postprocess our results

echo "workflow finished at $(date)"
```

Nice!  Try running your new script!

```
./blastp_workflow.sh
```

If we let it run to completion, it would take a while, so let's stop our script and add some things by **pressing Ctrl+C** to terminate the command.  We will use the time to add helpful features to our script and learn more about bash while we are at it.

## Reading command line arguments

What if we want to run our workflow on something other than "first10.pep"?  We could copy and edit our code, but we would end up with lots of copy of our code with lots of small edits.  How do we know which version is the latest or best to use?  The other option is to make our script generic by making the parts we want to change something we can specify when we run the workflow.

Let's make it so that we can give the query as a command line argument that would look like this:

```
./blastp_workflow.sh first10.pep
```

Bash has a number of special variables for working with command line arguments:

- $1 - the first command line argument ($2 would be the second, and so on)
- $@ - all arguments on the command line
- $# - the number of command line arguments
- $0 - the command name

Let's try them out!

Make a new script called "arguments.sh".  In it, put this

```
#!/bin/bash

echo "the command you ran was $0"
echo "you passed in $# arguments: $@"
```

We could be a bit more fancy about how we handle arguments using an if statement.  The syntax for an if statement looks like the following:

```
if [[ condition is true ]]; then
    # run this block of code
    echo "it's true!"
fi
```

We can also add `else` and `elif` code blocks:

```
if [[ condition is true ]]; then
    # run this block of code
    echo "it's true!"
elif [[ some other condition is true]]; then
	# run some other code
	echo "some other condition was true."
else
    echo "everything was false"
fi
```

The conditions themselves look something like this:

```
[[ $# -eq 1 ]]
```

That will be true if the number of arguments passed into the script was 1.  Here is a full list of conditional expressions: [https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html](https://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html)

## Hands-on

### 1) Update arguments.sh to do the following:
- `echo` a helpful comment if no arguments were passed in
- `echo` something nice and the name of the argument if 1 argument was passed in
- `echo` an error message if more than one argument was passed in and print all the arguments


### 2) Update blastp_workflow.sh to use a command line argument for the query AND check that you received one argument before running the workflow

- Hint: `exit` is a command that will quit the script.  By convention, when exiting with an error, you should give a non-zero exit code.  (e.g `exit 1`)
- Hint: you can set one variable to another.  So if I wanted to store the first command line argument in the variable `foo`, I could write: `foo=$1`


Previous: [Life Sciences Workflows](workflows1_1.md) | Next: [Automating Workflows 2](workflows1_3.md)
