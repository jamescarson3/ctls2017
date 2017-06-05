## The .bashrc

As you become more familiar with the system, there will be certain environment variable and module commands that you want to do every time you log in. You can automate this by putting the commands in your `.bashrc`.

The `.bashrc` is a hidden file in your home directory. Any file or directory with a single period `.` as the first character is hidden. To list all hidden files, you must use the `-a` flag with `ls`:
```
$ cd
$ ls -la
```

Any commands stored in your `.bashrc` are automatically executed each time you log in. To open up the `.bashrc` for editing, use VIM:
```
$ vim ~/.bashrc
```

Carefully read through the file. There is a section for loading modules, and a section for putting `export` commands to set environment variables. There is also an `alias` section for modifying your shell. Look at the commented lines (preceded by a `#` sign), for examples.


To make the changes take effect, you can either log out and log back in, or you can source the file:
```
$ source ~/.bashrc
```

Finally, as suggested in the `.bashrc` file, an alternative method for customizing your module environment is with the `module save` command:
```
$ module reset   # reset to system defaults
$ module load blast/2.2.31
$ module save
```

Now each time you log in, `blast/2.2.31` will automatically be loaded.


Note: TACC clusters primarily use `.bashrc` for issuing commands on log in. Other shells and other clusters may use a different file by default. If you are unsure, ask the administrator of the cluster.

### Exercise

1. Assuming you put `blast/2.2.31` into your default modules using `module save`, how do you undo that change?

[Click here for solution](intro_to_hpc_04_solution.md)

### Review of Topics Covered

| Command             | Effect     |
|---------------------|------------|
| `vim ~/.bashrc`     | edit log in commands and shell |
| `source ~/.bashrc`  | evaluate commands in `.bashrc` |
| `module reset`      | reset modules to system default |
| `module save`       | save current module configuration |


Previous: [Modules](intro_to_hpc_03.md) | Next: [Batch Job Submission](intro_to_hpc_05.md) | Top: [Course Overview](../../index.md)


