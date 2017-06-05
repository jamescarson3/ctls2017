## Network and File Transfers

In order to login or transfer files to a remote Linux file system, you must know the hostname (unique network identifier) and the username. If you are already on a Linux file system, those are easy to determine using the following commands:

```
$ whoami
wallen
$ hostname -f
login1.ls5.tacc.utexas.edu
```

Given that information, a user would remotely login to this Linux machine using the Terminal command:

```
$ ssh wallen@ls5.tacc.utexas.edu
(enter password)
(enter token)
```

Windows users would typically use the program "PuTTY" to perform this operation. Logging out of a remote system is done using the `logout` command, or the shortcut `<Ctrl+d>`:

```
  [ls5]$ logout
[local]$ 
```

Copying files from your local computer to Lonestar5 would require the `scp` command (Windows users use the program "WinSCP"):

```
[local]$ scp my_file wallen@ls5.tacc.utexas.edu:~/
(enter password)
(enter token)
```

In this command, you specify the name of the file you want to transfer (`my_file`), the username (`wallen`), the hostname (`ls5.tacc.utexas.edu`), and the path you want to put the file (`~/`). Take careful notice of the seperators including spaces, the @ symbol and the colon. Copy files from Lonestar5 to your local computer using ths following:

```
[local]$ scp wallen@ls5.tacc.utexas.edu:~/my_file ./
(enter password)
(enter token)
```

Instead of files, full directories can be copied using the "recursive" flag (`scp -r ...`). The `rsync` tool is an advanced copy tool that is useful for synching data between two sites. Although we will not go into depth here, example rsync usage is as follows:

```
$ rsync -azv local remote
$ rsync -azv remote local
```

This is just the basics of copying files. See example `scp` usage [here](https://en.wikipedia.org/wiki/Secure_copy) and example `rsync` usage [here](https://en.wikipedia.org/wiki/Rsync).



### Exercise

1. Identify which Lonestar5 login node you are on (login1, login2, login3)
2. Remotely login to a different Lonestar5 login node and list what files are available.
3. Logout until you are back to your original login node.
4. Copy the file `chr21.fa` to your local computer.

[Click here for solution](intro_to_linux_06_solution.md)

### Review of Topics Covered

| Command                    | Effect     |
|----------------------------|------------|
| `hostname -f`              | print hostname |
| `whoami`                   | print username |
| `ssh username@hostname`    | remote login |
| `logout`                   | logout of host |
| `scp local remote`         | copy a file from local to remote |
| `scp remote local`         | copy a file from remote to local |
| `rsync -azv local remote`  | sync files between local and remote |
| `rsync -azv remote local`  | sync files between remote and local |
| `<Ctrl+d>`                 | logout of host |



Previous: [More File Commands](intro_to_linux_05.md) | Next: [Miscellaneous Commands](intro_to_linux_07.md) | Top: [Course Overview](../../index.md)

