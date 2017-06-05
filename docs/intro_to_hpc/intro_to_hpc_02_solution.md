
1) Print the contents of the `PATH` environment variable.
```
$ echo $PATH
$ echo $PATH | tr ':' '\n'      # translates colons to newlines
```


2) What files exist in some of the directories found in the `PATH` environment variable?
```
$ ls -l /bin                # try some of these
$ ls -l /usr/bin
$ ls -l /usr/local/bin
$ ls -l /opt/apps/tacc/bin
```


3) Find an environment variable that stores your username.
```
$ env | grep "wallen"
```


4) Store Webster's dictionary in an environment variable called `DICTIONARY`.
```
$ echo $DICTIONARY        # nothing here yet
$ export DICTIONARY="$HOME/IntroToLinuxHPC/Lab01/websters.txt"
$ echo $DICTIONARY
/home1/03439/wallen/IntroToLinuxHPC/Lab01/websters.txt
$ head $DICTIONARY
A
a
aa
aal
...
```

[Return](intro_to_hpc_02.md)

