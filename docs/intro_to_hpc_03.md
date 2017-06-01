## Modules

Environment variables are finnicky, prone to typos, and a lot of work to edit manually. *Modules* make dynamically changing environment variables a lot easier and safer. Modules contain all the necessary environment variables for running a particular application or providing access to a particular library. In addition:

* A convenient way to dynamically change the user’s environment
* Avoid conflicts between program versions, compilers, libraries, etc.

Different clusters have different implementations of modules. More info on the TACC implementation of modules can be found [here](https://www.tacc.utexas.edu/research-development/tacc-projects/lmod)








To list all of your currently loaded modules:
```
$ module list
```

List all modules that are currently available to load:
```
$ module avail
```

Search for modules:
```
$ module avail blah
$ module spider blah
```

Show the contents of a module to see what effect loading it has:
```
$ module show modulename
```

Load and unload modules:
```
$ module load modulename
$ module unload modulename
```

Find more help on using module commands:
```
$ module help
```


### Exercise

1. Blah

[Click here for solution](intro_to_hpc_03_solution.md)

### Review of Topics Covered

| Command               | Effect     |
|-----------------------|------------|
| `module list`         | list currently loaded modules |
| `module avail`        | see what modules are available |
| `module avail name`   | search for module "name" |
| `module spider name`  | search for module "name" |
| `module show name`    | show the contents of module "name" |
| `module load name`    | load module "name" |
| `module unload name`  | unload module "name" |
| `module help`         | show module command help |


Previous: [Environment Variables](intro_to_hpc_02.md) | Next: [The .bashrc](intro_to_hpc_04.md)


