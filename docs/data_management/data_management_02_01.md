### What information is known about the files?

#### meta-data

* A file system relies on data structures described the files and not just the content of the files
* ***meta-data***: data that describes data or the relationship between data
* Each file is associated with an `inode`
  + integer number related to the meta-data
  + inodes store information such as
    * ownership
    * access mode (read, write, execute permissions)
    * file type (text, binary, data, compiled program)
  + inode number can be found with `ls -i` command.
    * add the inode to the first column

#### Example
```
$ mkdir test
$ cd test
$ touch bob
$ ln bob robert
$ ln -s bob bobby
$ ls -li
total 44
144170437511753087 -rw------- 2 beckbw G-814141    0 Jun  6 07:07 bob
144170437511753088 lrwxrwxrwx 1 beckbw G-814141    3 Jun  6 07:07 bobby -> bob
144170437511753087 -rw------- 2 beckbw G-814141    0 Jun  6 07:07 robert


$ stat bob robert bobby
$ stat *ob*
  File: `bob'
  Size: 0         	Blocks: 0          IO Block: 4194304 regular empty file
Device: dab3078h/229322872d	Inode: 144170437511753087  Links: 2
Access: (0600/-rw-------)  Uid: (827624/  beckbw)   Gid: (814141/G-814141)
Access: 2017-06-06 07:07:31.000000000 -0500
Modify: 2017-06-06 07:07:31.000000000 -0500
Change: 2017-06-06 07:07:40.000000000 -0500
 Birth: -
  File: `bobby' -> `bob'
  Size: 3         	Blocks: 0          IO Block: 4096   symbolic link
Device: dab3078h/229322872d	Inode: 144170437511753088  Links: 1
Access: (0777/lrwxrwxrwx)  Uid: (827624/  beckbw)   Gid: (814141/G-814141)
Access: 2017-06-06 07:07:46.000000000 -0500
Modify: 2017-06-06 07:07:46.000000000 -0500
Change: 2017-06-06 07:07:46.000000000 -0500
 Birth: -
  File: `robert'
  Size: 0         	Blocks: 0          IO Block: 4194304 regular empty file
Device: dab3078h/229322872d	Inode: 144170437511753087  Links: 2
Access: (0600/-rw-------)  Uid: (827624/  beckbw)   Gid: (814141/G-814141)
Access: 2017-06-06 07:07:31.000000000 -0500
Modify: 2017-06-06 07:07:31.000000000 -0500
Change: 2017-06-06 07:07:40.000000000 -0500
 Birth: -

```

* Different ways to determine the size and **age** of a file
  + `stat` display the access time, modification time, or meta-data change time
  + can also get the using `ls -u`, `ls -t`, or `ls -c`

```
$ ls -tl *ob*
lrwxrwxrwx 1 beckbw G-814141 3 Jun  6 07:07 bobby -> bob
-rw------- 2 beckbw G-814141 0 Jun  6 07:07 bob
-rw------- 2 beckbw G-814141 0 Jun  6 07:07 robert


$ find -mtime <days>
$ find -mtime 1
$
$ fine -mtime 0
./robert
./bob
./bobby
```

<hr>
#### What about file size?
#### First, Create some files to play with
`$cd test ` (if not already there)
```
$ for i in $(seq 0 10) ; do mkdir research_$i ; cd research_$i ; for j in $(seq 0 10) ; do touch  data_${i}_${j}; done; cd - ; done
$ tree
.
|-- bob
|-- bobby -> bob
|-- research_0
|   |-- data_0_0
|   |-- data_0_1
|   |-- data_0_10
|   |-- data_0_2
|   |-- data_0_3
|   |-- data_0_5
|   |-- data_0_7
|   |-- data_0_8
|   `-- data_0_9
|-- research_1
|   |-- data_1_0
|   |-- data_1_1
...
```
* Lets alter some files.
* We'll replace a file with random data
```
$ cat /dev/random > research_6/data_6_7
```
*** ctrl-c after a few seconds
* now how big is the file?
```
$ ls -lh research_6/data_6_7
```
* let's copy a pogram and overwrite a file then make it executable again (`chmod`)
```
$ cp /bin/ls research_5/data_5_6
$ chmod +x research_5/data_5_6
```
* now let's see how `find` explores the meta-data
```
$ find . -executable
$
$ find . -size +20M
$
$ find . -size +20k
```
* find will execute a command for each file it finds
```
$ find . -size +20k -exec ls -lh {} \;
```

### Example2: `du` disk Usage
* `du` will explore how much storage space a file or **group of files** takes up

```
$ du
4	./research_10
4	./research_7
4	./research_5
4	./research_0
4	./research_4
4	./research_9
27652	./research_6
4	./research_2
4	./research_8
4	./research_1
4	./research_3
27696	.
```
* can we make it human readable?
```
$ du -h
4.0K	./research_10
4.0K	./research_7
4.0K	./research_5
4.0K	./research_0
4.0K	./research_4
4.0K	./research_9
28M	./research_6
4.0K	./research_2
4.0K	./research_8
4.0K	./research_1
4.0K	./research_3
28M	.
'''
* what if I just want the grand total?
```
$ du -sh .
28M	.
```

<hr>

### Can I see how much of this disk is being used?
* use the `df` (disk free) command like we did earlier

```
$ df /home1
Filesystem                                                1K-blocks          Used      Available Use% Mounted on
129.114.54.5:/home1                                     13458257920    2000674816    10773943296  16% /home1
```
* or human readable:
```
$ df -h /home1
Filesystem           Size  Used Avail Use% Mounted on
129.114.54.5:/home1   13T  1.9T   11T  16% /home1
```

<hr>

### Quota : artificial limit place on you disk usage
* So now I know how big files and disks are. Is there a way to find how much I'm allowed to use?
* let's explore two commands: `quota` and `lfs quota`
  + `quota` will show you how much `/home1` you are using
  ```
  $ quota -s
Disk quotas for user beckbw (uid 827624):
     Filesystem  blocks   quota   limit   grace   files   quota   limit   grace
129.114.54.5:/home1
                  31076  10240M  10445M             198   1000k   1200k        
  ```
  + `lfs quota` is a LustreFS command that you can apply to Lustre mounted systems like $WORK and $SCRATCH

  ```
$ lfs quota -h $SCRATCH
Disk quotas for user beckbw (uid 827624):
     Filesystem    used   quota   limit   grace   files   quota   limit   grace
/scratch/03463/beckbw
                   164k      0k      0k       -     249       0       0       -
Disk quotas for group G-814141 (gid 814141):
     Filesystem    used   quota   limit   grace   files   quota   limit   grace
/scratch/03463/beckbw
                 54.58M      0k      0k       -     356       0       0       -

  ```


  <br>

  Prev: [Active data](data_management_01_04.md) | Next: [Module 3: Cleaning UP ](data_management_03_01.md) | UP: [Data Management Overview](data_management.md) | Top: [Course Overview](../../index.md)
