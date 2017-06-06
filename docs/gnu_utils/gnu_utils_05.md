# Manipulating and Formatting Files

Now that you know the basics for working with text files, you are ready to learn how to manipulate and format your output. You will specifically learn the following commands

- `paste` - combine columns
- `sort` - sort a file
- `diff` - compare files
- `sed` - search and replace
- `awk` - command line programming

### Combining Columns

`paste` joins files together by line with tabs by default.

```
$ cat A.txt
1
2
$ cat B.txt
A
B
$ paste A.txt B.txt
1  A
2  B
```

If you have worked with databases before, this is called an outer join. This command is useful to append information to regions in a bedgraph file.

```
$ paste fileA.bed fileB.bed
```

```
$ paste fileA.bed <( cut -f 3 fileB.bed )
```

### Sorting a File

Many programs or algorithms, such as bedtools, require or run more efficiently with sorted inputs. By default it will sort each line in ascending order.

```
$ sort fileA.bed
```

Did that do what you thought it would do? We can specifically tell it to sort on a column as well.

```
$ sort -k2 fileA.bed
```

It sorted `fileA.bed` on the second column, but its still out of order. Do you know why?

```
$ sort -k2n fileA.bed
```

Telling sort that the second column was a number finally got the output you were probably expecting. What happens when you you have more than one sequence name in the first column?

```
$ sort -k2n SRR2014925.bed | head -n 20
```

We can investigate this a little better with a pipeline

```
$ sort -k2n SRR2014925.bed | cut -f 1,2 | uniq | head
```

It looks like the file was only sorted by chromosome position, while the actual chromosome name was ignored. You can first sort by alphabetical name and then numerical position using the equivalent commands

```
$ sort -k1,1 SRR2014925.bed | sort -k2,2n | sort -k3,3n | uniq | head
```

```
$ sort -k1,1 -k2,2n -k3,3n SRR2014925.bed | uniq | head
```

Did that take a while?
Lets see if we can make it a little quicker.

If you look at how big the file is

```
$ du -sh SRR2014925.bed
   29M	SRR2014925.bed
```

and add some wiggle room, we can pre-allocate memory so no temporary files need to be created

```
$ sort -S 100M -k1,1 -k2,2n -k3,3n SRR2014925.bed | uniq | head
```

We can also assume that the sequence names have no unicode characters.

```
$ LC_ALL=C sort -S 100M -k1,1 -k2,2n -k3,3n SRR2014925.bed | uniq | head
```

#### Explore

- Sort `ecoli.gff3`
- Check to see which files are sorted
- Find any duplicate reads in `SRR2014925.bed`

### Comparing Files

The `diff` command is used to compare two text files. It can either give extremely basic output

```
$ diff -q fileA.bed fileA.bed
$ diff -q fileA.bed fileB.bed
```

or very specific output.

```
$ diff fileA.bed fileA.bed
$ diff fileA.bed fileB.bed
```

If you've ever used github, this output, or more specifically

```
$ diff -u fileA.bed fileB.bed
```

looks pretty familiar. This is how changes from an original file are tracked. Lets take a look at two more files.

```
$ diff fileA.bed fileC.bed
```

These files appear to be different, but look again.

```
$ diff <( sort -k1,1 -k2,2n fileA.bed ) <( sort -k1,1 -k2,2n fileC.bed )
```

These files contain the same lines, just in a different order. This is one of those cases where sort helps.

#### Explore

- Try to find where `fileB.bed` came from in SRR2014925.bed
- Try patching a file you make changes to with `patch`

### Search and Replace

When you need to make bulk changes to file, the `sed` command works great to search and replace regions of text.
It also comes with a fairly [extensive manual](https://www.gnu.org/software/sed/manual/sed.html), so we will only cover the basics.

#### Search and replace

The simplest version of a `sed` command takes the form of

```
sed -e "s/[look for]/[replace with]/" input.txt
```

Where

- `-e` tells `sed` to operate using the expression in quotes
  - Multiple `-e` expressions can be chained together
- `s` says we want to substitute `[look for]` with `[replace with]` on each line

I often use this to rename chromosomes.

```
$ sed -e "s/NZ_CP013025.1/Chr1/" fileA.bed
```

You can even make this change in-place with the `-i` argument

```
$ sed -i "s/NZ_CP013025.1/Chr1/" fileA.bed
$ head fileA.bed
```

#### Search and delete

You can also use sed to delete matching regions. This could be by replacing matching text with nothing

```
$ sed -e "s/;.*//" ecoli.gff3 | head
```

or deleting whole lines that match the text

```
sed -e "/^#/d" ecoli.gff3 | head
```

#### Explore

- Replace all the tabs in `fileA.bed` with commas
- Convert `SRR2014925_1.fastq` into a FASTA file

### AWK Programming

At this point, even without realizing it, you have done some BASH programming.
As you try to create complex workflows you may run into some of the limitations of BASH.
The AWK is a good way to perform math and complex formatting.

A basic awk program looks like

```
$ awk 'BEGIN { print "START" } { print } END { print "STOP"  }' fileC.bed
```

Which can be expanded into 3 sections:

1. `BEGIN { print "START" }`
  - Do this once at the start of the program
  - Usually used to print a header or initialize variables
2. `{ print }`
  - Do this (print) for each line in the file
3. `END { print "STOP"  }`
  - Do this after reading the whole file

AWK works with tab delimited input just like cut, so pulling out select regions is trivial. Insead of using `-k` use `$column_number`.

```
$ awk 'BEGIN { print "START" } { print $2 } END { print "STOP"  }' fileC.bed
```

You can also pull out multiple columns by simply printing the appropriate columns.

```
$ awk 'BEGIN { print "START" } { print $2 $3 } END { print "STOP"  }' fileC.bed
```

AWK will even recognize when a column is a number, so you can do math!

```
$ awk 'BEGIN { print "START" } { print $2+1 } END { print "STOP"  }' fileC.bed
```

You can even add completely columns somewhat like you did with paste.

```
$ awk 'BEGIN { print "START" } { print $0"\tC4" } END { print "STOP"  }' fileC.bed
```

You can keep track of the number of lines by

- initializing the `nLines` variable
- incrementing (`+=1`) `nLines` for each line
- printing `nLines` in the output

```
$ awk 'BEGIN { print "START"; nLines=0 } { nLines+=1; print $0"\t"nLines } END { print "STOP"  }' fileC.bed
```

or values by incrementing by a **column value** instead of a fixed number.

```
$ head SRR2014925.bedgraph | awk 'BEGIN { SUM=0; } { SUM+=$4; print $0 } END { print "Total = "SUM  }'
```

with variables. AWK even has some handy built-in variables that are updated while reading the file.

| Variable | Value |
|----------|-------|
| NR | Number of records (lines) |
| NF | Number of fields in record |

```
$ head SRR2014925.bedgraph | awk '{ print $0 } END { print NR" Records" }'
```

You can also do floating point operations.

```
$ head SRR2014925.bedgraph | awk 'BEGIN { SUM=0; } { SUM+=$4; print $0 } END { print "Total = "SUM/NR  }'
```

AWK is a whole scripting language, so you can read whole books on its capabilites.
Luckily, it's installed on every UNIX-like machine, so most answers already lie on the internet.
I do want to share one last useful trick for interacting with files.
AWK comparisons allow you to filter by value.

```
$ head SRR2014925.bedgraph | awk 'BEGIN { print "Coverages greater than 300"; } $4 > 300 '                                                           
```

You can apply this to location ranges too.

If you master AWK you will be ready to generate many useful file statistics right from the command line.

#### Explore

- Transform `ecoli.gff3` into a BED file
  - Pull out specific columns
  - Change indexing
- Calculate the average sequence depth for `NZ_CP013025.1` from `SRR2014925.bedgraph`
  - You will need to use a sum variable and NR after some grepping

## Extra Inspiration

- [Bioinformatics one-liners](https://github.com/stephenturner/oneliners)
- [CLI for NGS](http://userweb.eng.gla.ac.uk/umer.ijaz/bioinformatics/linux.html)

## Application

Here is a real-worl pipeline that you can use with the data we downloaded.

First, load the necessary modules and generate some index files.

```
$ module load samtools bwa bedtools

$ bwa index ecoli.fasta
$ samtools faidx ecoli.fasta
$ bedtools makewindows -g ecoli.fasta.fai -w 1000 > ecoli.bed
```

#### Align reads
```
$ bwa mem -t 24 ecoli.fasta SRR*_[12].fastq > aligned.sam
```

#### Convert to BAM

```
$ bwa mem -t 24 ecoli.fasta SRR*_[12].fastq | samtools view -bS - > aligned.bam
```

#### Convert to bed

```
$ bwa mem -t 24 ecoli.fasta SRR*_[12].fastq | samtools view -bS - | bedtools bamtobed -i - | cut -f 1-3 > aligned.bed
```

#### Pull out reads that map to genome

```
$ bwa mem -t 24 ecoli.fasta SRR*_[12].fastq | samtools view -bS - | bedtools bamtobed -i - | cut -f 1-3 | grep "^NZ_CP013025.1" > genome.bed
```

#### Calculate sequencing coverage

```
bwa mem -t 24 ecoli.fasta SRR*_[12].fastq | samtools view -bS - | bedtools bamtobed -i - | cut -f 1-3 | grep "^NZ_CP013025.1" | bedtools intersect -a ecoli.bed -b - -c > coverage.bedgraph
```

#### Calculate average sequencing coverage

```
bwa mem -t 24 ecoli.fasta SRR*_[12].fastq | samtools view -bS - | bedtools bamtobed -i - | cut -f 1-3 | grep "^NZ_CP013025.1" | bedtools intersect -a ecoli.bed -b - -c | awk 'BEGIN {sum=0;} {sum+=$4;} END {print "Average Coverag: "sum/NR"x";}'
```

#### DONE!

<br>
<br>

[Back - Redirection](gnu_utils_04.md) &nbsp;&nbsp;&#151;&nbsp;&nbsp; [Next - Course Overview](../../index.md)
