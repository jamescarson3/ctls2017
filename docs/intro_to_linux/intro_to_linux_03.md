## Creating and Manipulating Files

We have seen how to navigate around the filesystem and perform operations with folders. But, what about files? Just like on Windows or Mac, we can easily create new files, copy files, rename files, and move files to different locations. First, we will navigate to the home directory and create a few new files with the `touch` command:

```
$ cd          # cd on an empty line will automatically take you back to the home directory
$ pwd
/home1/03439/wallen
$ touch file_a
$ touch file_b
$ touch file_c
$ ls
file_a  file_b  file_c  folder1  folder2  folder3
```

These files we have created are all empty. Removing a file is done with the `rm` (remove) command. Please note that on Linux file systems, there is no "Recycle Bin". Any file or folder removed is gone forever and often un-recoverable:

```
$ touch junkfile
$ rm junkfile
```

Moving files with the `mv` command and copying files with the `cp` command works similar to how you would expect on a Windows or Mac machine. The context around the move or copy operation determines what the result will be. For example, we could move and/or copy files into folders:

```
$ mv file_a folder1/
$ mv file_b folder2/
$ cp file_c folder3/
```

Before listing the results with `ls` or `tree`, try to guess what the result will be.

```
$ tree .
.
|-- file_c
|-- folder1
|   |-- file_a
|   |-- subfolderA
|   |-- subfolderB
|   `-- subfolderC
|-- folder2
|   `-- file_b
`-- folder3
    `-- file_c
```

Two files have been moved into folders, and `file_c` has been copied - so there is still a copy of `file_c` in the home directory. Move and copy commands can also be used to change the name of a file:

```
$ cp file_c file_c_copy
$ mv file_c file_c_new_name
```

By now, you may have found that Linux is very unforgiving with typos. Generous use of the `<Tab>` key to auto-complete file and folder names, as well as the `<UpArrow>` to cycle back through command history, will greatly improve the experience. As a general rule, try not to use spaces or strange characters in files or folder names. Stick to:

```
A-Z     # capital letters
a-z     # lowercase letters
0-9     # digits
-       # hyphen
_       # underscore
.       # period
```

### Exercise

1. Navigate to your home directory
2. Execute this exact command: `cp -r /work/03439/wallen/public/challenge02 ./`
3. Navigate into the `challenge02` folder.
4. Somewhere within there is a file. Can you find it?
5. Advanced Linux users: What command can be used to generate this hierarchy of folders?

[Click here for solution](intro_to_linux_03_solution.md)


### Review of Topics Covered

| Command                    | Effect     |
|----------------------------|------------|
| `touch file_name`          | create a new file |
| `rm file_name`             | remove a file |
| `rm -r dir_name/`          | remove a directory |
| `mv file_name dir_name/`   | move a file into a directory |
| `mv old_file new_file`     | change the name of a file |
| `mv old_dir/ new_dir/`     | change the name of a directory |
| `cp old_file new_file`     | copy a file |
| `cp -r old_dir/ new_dir/`  | copy a directory |
| `<Tab>`                    | auto complete file or folder names |
| `<UpArrow>`                | cycle through command history |


Previous: [Looking and Moving Around](intro_to_linux_02.md) | Next: [Looking at the Contents of Files](intro_to_linux_04.md) | Top: [Course Overview](../../index.md)

