### Data Duplication/Deplication

#### Duplication can aid consistency
* Following a template structure and naming convention allows you to:
  + develop consistent scripts and datasets.
  + ** EXAMPLE ** :
  + Given `mustard/pdb`, `mustard/docking`,
  `strawberry/pdb`, and `strawberry/docking`, you can archive all docking results via:
    * `$ tar -cvzf docking_results.tar.gz */docking`
  + Better to copy and modify an existing file instead of editing from scratch.
    * less chance of typographical errors

#### De-duplication
* Minimizing identical De-duplication
  + Avoids excessive disk usage and uses less file space
  + Avoids accidental content changes for more consistent analyses
  + Promotes future clean-up and de-duplication
    * *clean as you go*
* **EXAMPLE** :
  + In our `test` folder, let's pretend all data_x_6 files are duplicates source files
  + We could use the `find` command with the `-exec` option can be used to remove them all
  ```
  $ find test -name data_*_6 -print -exec rm {} \;
  ```
* **Protecting yourself from unintentional file removal**
  + recall our earlier `chmod` discussion
  + We can stop write (also delete) and execute privileges
```
$ chmod -wx test/*/data_*_3
$ rm test/*/data_*_3
rm: remove write-protected regular empty file `test/research_0/data_0_3'?
```
*ctrl-c*


#### Ways of Avoiding Duplication
* Use symbolic links ( `ln -s`) instead of copying, if possible
* **EXAMPLE** :
```
$ ln -s mustard/flower/control_group.db mustard/leaf/
```

* **When avoid duplication, don't trivially install common software into you `$HOME` **
 + ** QUIZ: what is your `/home` quota ?
 + Avoid placing common software, especially executables in `/home`
   * `/home` quota is small ( 5 GB)
   * `/home` has worse I/O performance than `$WORK` or `$SCRATCH`
   * Executables in `/home` that start/stop quickly during an HPC job have been known to dramatically decrease performance for all users of `/home`.
   * The admins might kill you job.
  + Use `$WORK` instead.

  <br>

  Prev: [Best Practices](data_management_04_01.md) | UP: [Data Management Overview](data_management.md) | Top: [Course Overview](../../index.md)
