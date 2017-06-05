## Environment Variables

On a Linux system, environment variables are *variables that are defined in the current shell, and can be passed into processes that the shell spawns*. They have many practical purposes, including but not limited to:

* Point to the locations of executables
* Point to the locations of libraries
* Point to other special locations in the shell
* Provide information about the user to the programs
* Provide other special information to programs

To print all of the environment variables currently defined in your shell, use the `env` command:
```
$ env
```

There are quite a few, many of which you will never need to use. There are some important ones, however. To filter the output, you can print the contents of a specific variable. Use the `echo` command to print the contents of an environment variable called `PATH` or the `env | grep` combination::
```
$ echo $PATH
$ env | grep PATH
```

Note: The name of the variable is `PATH`; use `$PATH` to access the contents of the variable. You can also manually edit the content of environment variables using the `export` command:
```
$ echo BLAH                     # this is the variable itself
$ echo $BLAH                    # use $ to access the contents
$ export BLAH="some text here"
$ echo $BLAH
```

You can edit existing variables as well. The `PATH` variable, which defines which executables are available to you in your current shell, is often edited by users. We should be careful editing it because it stores the location of our very common commands like `ls` and `cd`. If we lose those paths, then it will be difficult to execute commands. Edit the beginning or the ending of the `PATH` variable as follows (contents at the beginning supersedes contents at the end):
```
$ export PATH=$PATH:/new/path/to/add
$ export PATH=/new/path/to/add:$PATH
```

Environment variables can be reset by logging out and in:
```
$ logout
```


### Exercise

1. Print the contents of the `PATH` environment variable.
2. What files exist in some of the directories found in the `PATH` environment variable?
3. Find an environment variable that stores your username.
4. Store Webster's dictionary in an environment variable called `DICTIONARY`.

[Click here for solution](intro_to_hpc_02_solution.md)

### Review of Topics Covered

| Command                  | Effect     |
|--------------------------|------------|
| `env`                    | print all environment variables |
| `echo $VAR`              | print the contents of an the environment variable "VAR" |
| `export VAR="value"`     | set an environment variable "VAR" to "value" |
| `env | grep "PATTERN"`   | search for "PATTERN" among environment variables | 



Previous: [Introduction to HPC](intro_to_hpc_01.md) | Next: [Modules](intro_to_hpc_03.md) | Top: [Course Overview](../../index.md)


