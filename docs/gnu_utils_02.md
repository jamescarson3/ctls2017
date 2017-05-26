# Viewing Text Files

Most bioinformatics data formats are simple ASCII text files. Everything from the original `FASTA` reference and `FASTQ` reads to the aligned `SAM` reads and summarized `BED` files. There are many more, but we're going to focus on these.

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

You can also print multiple files at once with the cat command.

```
$ cat fileA.txt fileB.txt
```

Notice that files are printed in the order you specify on the command line.

```
$ cat fileB.txt fileA.txt
```

### Printing part of a file

For times when the whole file is too much information, you can print the first few lines using the `head` command.

```
$ head fileA.txt
```

You can also print the last few lines of the file with the `tail` command.

```
$ tail fileA.txt
```


You can also control the number of lines you want printed with the `-n` argument.

```
$ head -n 2 fileA.txt
$ tail -n 2 fileA.txt
```

#### Explore

* How many lines get printed by default?
* What happens when you file has fewer lines?
* Find other userful parameters by looking at the documentation (`man head`).

### Browsing through a file

Instead of printing an entire file, or a specific part of a file, you can also browse though it with the `less` command.

```
$ less fileA.txt
```

You can
* move lines with the arrow kays
* skip lines with the spacebar
* regex search with `/`
* quit by pressing `q`

The more you use less, the more you will appreciate less. :smile:

### Text vs Binary

While most files are text format, you can encounter binary files that will break your workflow. What would that look like?

```
$ head SRR2014925.sam
```

```
$ head SRR2014925.bam
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

## Exercises
- Print the first 2 reads of a fastq file
- Print the last read of a fastq file
- What chromosome in `reference.fa` has 4 CATs in a row?

<table width="100%" border="0"><tr>
<td align="left"><a href="gnu_utils_01.html">Introduction</a></td>
<td align="center">Viewing Files</td>
<td align="right"><a href="gnu_utils_03.html">Filtering Files</a></td>
</tr></table>
