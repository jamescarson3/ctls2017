### How do I move my compress data off site

* Recall the previous discussions of `scp`
* we can transfer a compress archive much faster and easier than an intact directory tree:

#### EXAMPLE: transferring out .tar.gz file to our laptops

```
$ scp <USER>@<ORIG_HOSTNAME>:/old/path/filename <USER>@<DESTINATION_HOSTNAME:/path/filename
$ scp beckbw@ls5.tacc.utexas.edu:/work/03463/beckbw/lonestar/test.tar.gz .
```

* Let's test it!
  + QUESTION: How can I view the contents of a tarball?

* on my laptop (your screen may vary)
```
$ tar -tvf test.tar.gz
```

### RANCH Tape Robot
* We don't have allocations on RANCH, but you use similar steps to stage data to the robot:
```
$ scp myfile ${ARCHIVER}:${ARCHIVE}/myfile
```


  <br>

  Prev: [Cleaning Up ](data_management_03_01.md) | Next: [Module 4: Best Practices](data_management_04_01.md) | UP: [Data Management Overview](data_management.md) | Top: [Course Overview](../../index.md)
