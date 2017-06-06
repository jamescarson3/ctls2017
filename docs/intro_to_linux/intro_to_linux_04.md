## Looking at the Contents of Files

Everything we have seen so far has been with empty files and folders. We will now start looking at some real data. Navigate to your home directory, then issue the following `cp` command to copy a "tar archive" file from me:

```
$ cd ~     # the tilde ~ is also a shortcut referring to your home directory
$ pwd
/home/03439/wallen
$ cp /work/03439/wallen/public/IntroToLinuxHPC.tar .
```

Try to use `<Tab>` to autocomplete the name of the file. Do NOT change the username or lustre number to your username and lustre number - in this case you are copying a file from my directory to your directory. Also, please notice the single dot `.` at the end of the copy command, which indicates that you want to cp the tar archive to `.`, this present location (your home directory).

This archive file is actually a bundle of many files and folders, all packed into one nice, easily transportable object. Once it is copied over, un-pack the file with the following command:

```
$ ls
IntroToLinuxHPC.tar
$ tar -xvf IntroToLinuxHPC.tar
```

In the first lab (`Lab01`), we have a file called `websters.txt`. This a list of all the words in Webster's Dictionary. But how can we see the contents of the file?

```
$ cd IntroToLinuxHPC
$ cd Lab01
$ pwd
/home1/03439/wallen/IntroToLinuxHPC/Lab01
$ ls
README websters.txt
```

If you want to see the contents of a file, use the `cat` command to print it to screen:

```
$ cat websters.txt
A
a
aa
aal
aalii
aam
Aani
aardvark
...
```

This is a long file! Printing everything to screen is much too fast and not very useful. We can use a few other commands to look at the contents of the file with `more` control:

```
$ more websters.txt
```

Press the `<Enter>` key to scroll through line-by-line, or the `<Space>` key to scroll through page-by-page. Press `q` to quit the view, or `<Ctrl+c>` to force a quit if things freeze up. A `%` indicator at the bottom of the screen shows your progress through the file. This is still a little bit messy and fills up the screen. The `less` command has the same effect, but is a little bit cleaner:

```
$ less websters.txt
```

Scrolling through the data is the same, but now we can also search the data. Press the `/` forward slash key, and type a word that you would like to search for. The screen will jump down to the first match of that word. The `n` key will cycle through other matches, if they exist.

Finally, you can view just the beginning or the end of a file with the `head` and `tail` commands. For example:

```
$ head websters.txt
$ tail websters.txt
```

The `>` and `>>` shortcuts in Linux indicate that you would like to redirect the output of one of the commands above. Instead of printing to screen, the output can be redirected into a file:

```
$ cat websters.txt > websters_new.txt
$ head websters.txt > first_10_lines.txt
```

A single greater than sign `>` will redirect and **overwrite** any contents in the target file. A double greater than sign `>>` will redirect and **append** any output to the end of the target file.


One final useful way to look at the contents of files is with the `grep` command. `grep` searches a file for a specific pattern, and returns all lines that match the pattern. For example:

```
$ grep "banana" websters.txt
banana
cassabanana
```

Although it is not always necessary, it is safe to put the search term in quotes. More on `grep` later.


### Exercise

1. Extract every word from `websters.txt` that contains the string `apple`, and put it into a new file called `apple.txt`.
2. Extract every word from `websters.txt` that contains the string `carrot`, and put it into a new file called `carrot.txt`.
3. Extract every word from `websters.txt` that contains the string `cheese`, and put it into a new file called `cheese.txt`.
4. Examine the contents of `apple.txt`, `carrot.txt`, and `cheese.txt` to make sure they contain what you expect.
5. Concatenate all three lists into a new file called `food.txt`.
6. Advanced Linux users: can you do all of the above, and alphabetize the output in one command?

[Click here for solution](intro_to_linux_04_solution.md)

### Review of Topics Covered

| Command                     | Effect     |
|-----------------------------|------------|
| `cat file_name`             | print file contents to screen |
| `cat file_name >> new_file` | redirect output to new file |
| `more file_name`            | scroll through file contents |
| `less file_name`            | scroll through file contents |
| `head file_name`            | output beginning of file |
| `tail file_name`            | output end of file |
| `grep pattern file_name`    | search for 'pattern' in a file |
| `~/`                        | shortcut for home directory |
| `<Ctrl+c>`                  | force interrupt |
| `>`                         | redirect and overwrite |
| `>>`                        | redirect and append |


Previous: [Creating and Manipulating Files](intro_to_linux_03.md) | Next: [More File Commands](intro_to_linux_05.md) | Top: [Course Overview](../../index.md)

