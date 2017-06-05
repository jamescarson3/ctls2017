## Miscellaneous Commands

Some say the only command you ever need to memorize is `man`. This command brings up the manual page for any other command. For exampe, try issuing:

```
$ man ls
```

Navigate the manual page by pressing `<Enter>` to scroll down line-by-line, or `<Ctrl+u>` or `<Ctrl+d>` to page up or page down. The `q` key or `<Ctrl+c>` can be used to exit. Take note of all the different flags that come with `ls`.

The commands `echo` and `date` will be useful later to print output control during batch job execution. For example, try the commands:

```
$ echo "The current date and time is:"
$ date
```

The `which` command tells the user the location of a command or program that is currently in the "PATH" (more on this later). For example, we can find the location of the `ls` command, or help determine the version of python that is in our PATH:

```
$ which ls
/bin/ls
$ which python
/usr/bin/python
$ python --version
Python 2.6.9
```

Finally, the `history` command prints your command line history. It is useful to scroll through previous commands:

```
$ history
```

### Exercise

1. Use the `date` command to print the Coordinated Universal Time (UTC time zone).
2. Use the `date` command to just print the month.
3. What does the `cal` command do? Show some different examples.
4. What does the `seq` command do? Show some different examples.

[Click here for solution](intro_to_linux_07_solution.md)

### Review of Topics Covered

| Command                | Effect     |
|------------------------|------------|
| `man command`          | bring up manual for "command" |
| `echo "this sentence"` | print a statement to standard out |
| `echo "this" >> file`  | print a statement into a file |
| `date`                 | print system date and time |
| `which command`        | print location of "command" |
| `history`              | show command history |


Previous: [Network and File Transfers](intro_to_linux_06.md) | Next: [Text Editing with VIM](intro_to_linux_08.md) | Top: [Course Overview](../../index.md)

