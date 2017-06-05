## Looking and Moving Around

On a Windows or Mac desktop, our present location determines what files and folders we can access. I can "see" my present location visually with the help of the graphic interface - I could be looking at my Desktop, or the contents of a folder, for example. In a Linux command-line interface, we lack the same visual queues to tell us what our location is. Instead, we use a command - `pwd` (print working directory) - to tell us our present location. Try executing this command on Lonestar5:

```
$ pwd
/home1/03439/wallen 
```

This home location on the Linux filesystem is unique for each user, and it is roughly analogous to C:\Users\username on Windows, or /Users/username on Mac.

To see what files and folders are available at this location, use the `ls` (list) command:

```
$ ls
```

I have no files or folders in my home directory yet, so I do not get a response. We can create some folders using the `mkdir` (make directory) command. The words 'folder' and 'directory' are interchangeable:


```
$ mkdir folder1
$ mkdir folder2
$ mkdir folder3
```

```
$ ls
folder1  folder2  folder3
```

Now we have some folders to work with. To "open" a folder, navigate into that folder using the `cd` (change directory) command. This process is analogous to double-clicking a folder on Windows or Mac:

```
$ pwd
/home1/03439/wallen
$ cd folder1
$ pwd
/home1/03439/wallen/folder1
```

Now that we are inside folder1, make a few sub-folders:

```
$ mkdir subfolderA
$ mkdir subfolderB
$ mkdir subfolderC
$ ls
subfolderA  subfolderB  subfolderC
```

Use `cd` to Navigate into `subfolderA`, then use `ls` to list the contents. What do you expect to see?

```
$ cd subfolderA
$ pwd
/home1/03439/wallen/folder1/subfolderA
$ ls
```

There is nothing there because we have not made anything yet. Next, we will navigate back to the home directory. So far we have seen how to navigate "down" into folders, but how do we navigate back "up" to the parent folder? There are different ways to do it. For example, we could specify the complete path of where we want to go:

```
$ pwd
/home1/03439/wallen/folder1/subfolderA
$ cd /home1/03439/wallen/folder1
$ pwd
/home1/03439/wallen/folder1/
```

Or, we could use a shortcut, `..`, which refers to the **parent folder** - one level higher than the present location:

```
$ pwd
/home1/03439/wallen/folder1
$ cd ..
$ pwd
/home1/03439/wallen
```

We are back in our home directory. Finally, use the  `rmdir` (remove directory) command to remove folders. This will not work on folders that have any contents (more on this later):

```
$ mkdir junkfolder
$ ls 
folder1 folder2 folder3 junkfolder
$ rmdir junkfolder
$ ls
folder1 folder2 folder3
```

A bonus command available on some Linux operating systems is called `tree`. (This is not found on your cheat sheet. Consider writing it in.) The `tree` command displays files and folders in a hierarchical view. Use another Linux shortcut, `.`, to indicate that you want to list files and folders in your **present location**.

```
$ tree .
.
|-- folder1
|   |-- subfolderA
|   |-- subfolderB
|   `-- subfolderC
|-- folder2
`-- folder3
```

### Exercise

1. Navigate to your home directory
2. Make a new folder called `challenge01`
3. Navigate into that new folder
4. Make 5 sub folders called `a`, `b`, `c`, `d`, `e`
5. Wihin each of those sub folders, make 5 sub folders called `1`, `2`, `3`, `4`, `5`
6. Navigate back to your home directory and print a hierarchical view of the `challenge01` folder
7. Advanced Linux users: can you do this on one line?


[Click here for solution](intro_to_linux_02_solution.md)

### Review of Topics Covered

| Command           | Effect     |
|-------------------|------------|
| `pwd`             | print working directory |
| `ls`              | list files and directories |
| `ls -l`           | list files in column format |
| `mkdir dir_name/` | make a new directory |
| `cd dir_name/`    | navigate into a directory |
| `rmdir dir_name/` | remove an empty directory |
| `tree`            | list files and directories hierarchically |
| `.` or `./`       | refers to the present location |
| `..` or `../`     | refers to the parent directory |


Previous: [Introduction to Linux](intro_to_linux_01.md) | Next: [Creating and Manipulating Files](intro_to_linux_03.md) | Top: [Course Overview](../../index.md)
