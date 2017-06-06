### How can I clean up my data?

* How old and/or inactive is your data?
* Is it time to archive it or transfer it?
  + Recall our prior discussions on
    * **Active Data**
    * **10 day policy** for $SCRATCH
  + Am I running short on quota?


* For any of these cases it might be a good time to clean up your data.
  + remove duplication
  + organize you data into archives
  + prepare you data for moving to different media or transferring across the network
  + compress your data to minimize
    * disk usage
    * network transfer or disk copy times

### Compression and archiving

* Recall the previous discussion on `gzip`, `gunzip`
* `gzip` compresses data by identifying blocks of identical data and replacing it with a smaller placeholder
* `gunzip` or `gzip -d` restores the file.

* `gzip` replaces the orginal with a compress version but we can keep both using the `-c` flag and a `redirect`

```
$ gzip -c file > file.gz
```
* The `-#` flag changes the compression level from:
  + 1 : weak but fast
  + ...
  + 9 : strong but slow.

#### Example: find the larger "random" file in the "test" directory and compress it at different level

```
$ cd research_6
$ for i in $(seq 1 9) ; do gzip -c -${i} data_6_7 > data_6_7_${i}.gz ;done
$ ls -lrsh
total 271M
  0 -rw------- 1 beckbw G-814141   0 Jun  6 02:34 data_6_9
  0 -rw------- 1 beckbw G-814141   0 Jun  6 02:34 data_6_8
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_9.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_8.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_7.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_6.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_5.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_4.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_3.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_2.gz
28M -rw------- 1 beckbw G-814141 28M Jun  6 08:30 data_6_7_1.gz
27M -rw------- 1 beckbw G-814141 27M Jun  6 02:37 data_6_7
```

#### DISCUSSION: Did compression save me anything?

<hr>

### Archiving and Transfering

* Recall our previous use of `tar` (Tape Archive)
  + create: `tar -cvf <file.tar> <files>`
  + extract: `tar -xvf <file.tar>`
  + list contents: `tar -tvf <file.tar>`

* Let's practice on the "test" directory
  + ** Can we use tar to "copy" files?
  + Let's create an tar archive and extract it elsewhere

```
$ cd $WORK
$ tar -cvf test.tar $HOME/test
```
##### MISTAKE: we have the `/home1` path in our archive

```
$ tar -cvf test.tar -C $HOME test
$ tar -tvf test.tar
```
* we could create then extract that archive to copy the files, but let's practice piping
```
$ cd $WORK
$ tar -cvf - -C $HOME test | tar -xvf -
```
* **We just used `tar` to copy an entire directory tree**


### Compressing Archives
* Earlier, we made a file called `test.tar` **BUT** we made a mistake: we forgot to compress using the `-z` option
  + `tar -cvzf <file.tar.gz> <files>`
* luckily we can compress at any time
```
$ gzip -9 test.tar
$ ls -rt
$ tar -tvzf test.tar.gz
```

  <br>

  Prev: [FS Info ](data_management_02_01.md) | Next: [Transferring](data_management_03_02.md) | UP: [Data Management Overview](data_management.md) | Top: [Course Overview](../../index.md)
