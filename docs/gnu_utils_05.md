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

```
$ du -sh SRR2014925.bed
   29M	SRR2014925.bed
```

We can pre-allocate memory so no temporary files need to be created

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

### Comparing Files

The `diff` command

### Search and Replace

### AWK Programming

At this point, even without realizing it, you have done some BASH programming.
As you try to create complex workflows you may run into some of the limitations of BASH.
The AWK is a good way to perform complex operations


## Exercises
- Use awk to transform a gff3 into a bed file
-
-
<br>
<br>

[Back - Redirection](gnu_utils_04.md) &nbsp;&nbsp;&#151;&nbsp;&nbsp; [Next - Agenda](welcome_01.md)
