## More File Commands

By now you have learned the basics of navigating the file system, as well as the most common file manipulation and reading commands. Now, we will cover a few advanced file commands that are useful to share, transport, and archive files.

Data compression is an easy way to save space and stay within your quota. Raw text data on Linux file systems can be made several factors smaller using the `gzip` tool. First, navigate to the `Lab02` directory:

```
$ pwd
/home1/03439/wallen/IntroToLinuxHPC/Lab01
$ cd ../Lab02
$ pwd
/home1/03439/wallen/IntroToLinuxHPC/Lab02
$ ls
Homo_sapiens.GRCh38.dna.chromosome.21.fa  README
```

Here we have a fasta file containing the DNA sequence of human chromosome 21. It is 41 MB in size. Make a copy of the file and change the name to something short so it is easier to work with:

```
$ cp Homo_sapiens.GRCh38.dna.chromosome.21.fa chr21.fa
$ ls -l
-rwx------ 1 wallen G-815499 42384874 May 26 12:59 chr21.fa*
-rwx------ 1 wallen G-815499 42384874 May 25 09:24 Homo_sapiens.GRCh38.dna.chromosome.21.fa*
-rwx------ 1 wallen G-815499      656 May 25 09:24 README*
```

The copy and original are identical in size. Use gzip to compress the copy:

```
$ gzip -v chr21.fa
chr21.fa:        72.2% -- replaced with chr21.fa.gz
```

The original file is automatically given a `.gz` extension, and on the command line (with the `-v` flag) the percent compression is reported. The file can be decompressed by using the `gunzip` command, or the `gzip` command with the `-d` flag:

```
$ gzip -dv chr21.fa.gz
chr21.fa.gz:     72.2% -- replaced with chr21.fa
```

A "tar archive" is a collection of files and directories all bundled up into a single file. This makes it easier to share, transport, and compress many files at once:

```
$ cd ../
$ pwd 
/work/03439/wallen/public/IntroToLinuxHPC
$ tar -cvf Lab02.tar Lab02/
Lab02/
Lab02/chr21.fa
Lab02/.gene_source
Lab02/README
Lab02/Homo_sapiens.GRCh38.dna.chromosome.21.fa
```

Now there is a new file called `Lab02.tar` which contains all the contents of the original `Lab02/` directory. To unarchive, use the `-x` flag instead of the `-c` flag:

```
$ mv Lab02.tar ~/
$ cd ~/
$ tar -xvf Lab02.tar
Lab02/
Lab02/chr21.fa
Lab02/.gene_source
Lab02/README
Lab02/Homo_sapiens.GRCh38.dna.chromosome.21.fa
$ cd -       # cd with a minus symbol returns you to the previous directory
```

Another way to save space on a Linux file system is with linking (`ln`) and permissions (`chmod`). For example, rather than making a copy of a reference library in every directory, you can create links to the reference genome:

```
$ cd $HOME
$ ln -s ./IntroToLinuxHPC/Lab02/chr21.fa ./chr21.fa
$ ls -l              # is chr21.fa in this location?
```

Also, you can share reference libraries with your coworkers using `chmod`:

```
$ cd IntroToLinuxHPC/Lab02/
$ ls -l
 # examine output before
$ chmod 755 chr21.fa
$ ls -l
 # examine output after
```

There will be more on linking and changing permissions in the context of Data Management later on.

### Exercise

1. How large is `Homo_sapiens.GRCh38.dna.chromosome.21.fa` before and after compression?
2. How large is `websters.txt` before and after compression?
3. Assuming the same compression rate, how large will 1 TB of text files be after compression?

[Click here for solution](intro_to_linux_05_solution.md)

### Review of Topics Covered

| Command                 | Effect     |
|-------------------------|------------|
| `gzip -v file`          | compress a file |
| `gzip -dv file`         | decompress a file |
| `tar -cvf archive dir/` | create an archive |
| `tar -xvf archive`      | extract the contents of an archive |
| `ln -s target link`     | link files or directories |
| `chmod 755 file`        | change file permissions |
| `chmod -R 755 dir/`     | change permissions recursively |


Previous: [Looking at the Contents of Files](intro_to_linux_04.md) | Next: [Network and File Transfers](intro_to_linux_06.md) | Top: [Course Overview](../../index.md)

