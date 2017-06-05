

1) Navigate to your home directory

2) Execute this exact command: `cp -r /work/03439/wallen/public/challenge02 ./`

3) Navigate into the `challenge02` folder.

```
$ cd
$ pwd
/home1/03439/wallen
$ cp -r /work/03439/wallen/public/challenge02 ./
$ cd challenge02
```

4) Somewhere within there is a file. Can you find it?

```
$ cd dir0/folder0/subfolder0/
$ ls                            # doing it manually would take forever
$ cd ../../../
```

```
$ ls dir0/folder0/subfolder0/   # this saves a few steps, would still take a long time
```

```
$ tree ./           # use tree to print a file hierarchy and scroll through
$ find . -type f    # what do you think this command is doing?
```

5) Advanced Linux users: What command can be used to generate this hierarchy of folders?
```
for V1 in `seq 0 9`; do for V2 in `seq 0 9`; do for V3 in `seq 0 9`; do mkdir -p dir${V1}/folder${V2}/subdir${V3}; done; done; done
```


[Return](intro_to_linux_03.md)
