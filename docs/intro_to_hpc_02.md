# Environment Variables


Definition: Variables that are defined in the current shell, and can be passed into processes that the shell spawns.

* Point to the locations of executables
* Point to the locations of libraries
* Point to other special locations in the shell
* Provide information about the user to the programs
* Provide other special information to programs

Print current environment variables:
```
$ env
```

Print the contents of a specific variable:
```
$ echo $PATH
$ env | grep PATH
```

Define new or edit existing environment variables (contents at the beginning supersedes contents at the end):
```
$ export PATH=$PATH:/new/path/to/add
$ export PATH=/new/path/to/add:$PATH
```

Environment variables reset by logging out and in:
```
$ logout
```


## Assesment Challenge:

1. Blah

[Click here for solution](intro_to_hpc_02_solution.md)

## Review of Topics Covered:
 * Network and file transfers (`hostname, whoami, ssh, scp, rsync`)

| Command                    | Effect     |
|----------------------------|------------|
| `echo $VAR`            | print the contents of an the environment variable "VAR" |
| `export VAR="value"`   | set an environment variable "VAR" to "value" |
| `env`                  | print all environment variables |
| `env \| grep pattern`  | search for "PATTERN" among environment variables | 



Previous: [Introduction to HPC](intro_to_hpc_01.md) | Next: [Modules](intro_to_hpc_03.md)


