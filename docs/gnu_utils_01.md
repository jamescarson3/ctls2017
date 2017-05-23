# Introduction to GNU Coreutils

The GNU Core Utilities are the basic file, shell and text manipulation utilities of the GNU operating system.
These are the core utilities which are expected to exist on every Unix-like operating system.

The skills that you learn here will be useful on _every_ Mac, Linux, HPC, and now even Windows machine that your workflows could run on.

Time - 90 minutes

Inspiration from http://swcarpentry.github.io/shell-novice/04-pipefilter/

### Questions
* How can I analyze data using existing commands?

### Objectives
* Read and identify text files.
* Filter and format a text file.
* Redirect output from a command to a file.
* Construct command pipelines with two or more stages.
* Explain what usually happens if a program or pipeline isn’t given any input to process.

# Text Files

Most bioinformatics data formats are simple ASCII text files. Everything from the original `FASTA` reference and `FASTQ` reads to the aligned `SAM` reads and summarized `BED` files. There are many more, but we're going to focus on these.

## Viewing Text Files
You already know how to discover files with the `ls` and `find` commands, but you can also read them without opening them in a file editor. The main commands for doing this are

- `cat`
- `head`
- `tail`
- `less`

### Printing a whole file
When necessary, you can print an entire file with the `cat` command. This is great to quickly print an entire file.
```
$ cat some_file.txt
```
### Printing part of a file

### Browsing through a file

## Text vs Binary

While most files are text format, you can encounter binary files that will break your workflow. What would that look like?

```
$ head sample.sam
```

```
$ head sample.bam
```

Notice that printing out the non-ASCII characters in the binary BAM will corrupt your terminal window. The quickest way to fix this is by resetting it.

```
$ reset
```

You will learn to recognize which file formats are text vs binary, but you can always check with the `file` command, which doesn't corrupt your terminal.

```
$ file SRR2014925.sam
SRR2014925.sam: ASCII text, with very long lines

$ file SRR2014925.bam
SRR2014925.bam: gzip compressed data, extra field
```

## Filtering a text File
The contents of a text file can be filtered to either show a region of interest or provide a summary of the file.

- `cut`
- `sort`
- `grep`

## Redirecting and Piping Output
While its great to print sorted output to the command line, it would be great if you could save it as you would a text editor.

- `>`
- `<`
- `|`

## Manipulating and formatting a Text File
As data scientists, much of your time consists of formatting data for processing. This could mean appending fields in a file when they don't exist, forcing naming schemes to match between versions, or just simply formatting a file in a standard way.

- `paste`
 - Add a column to a bedgraph
- `sed`
 - Change chr1 to 1
- `awk`
 - Add a unique name
 - format text
 - math

## Exercises
- GFF3 -> bed
- fastq -> fasta
- parallel merge sort a bedgraph
-
