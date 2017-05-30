# Filtering Text Files

Often times, you will want specific information from your data.
This could be specific columns from a file or select information.

Three of the most versitile commands for investigating bioinformatics files are

- `cut` - selecting columns
- `grep` - selecting words
- `uniq` - selecting unique information

We will be using the data you already generated for viewing files. If you no longer have these files, plese [go back](gnu_utils_02.md) and regenerate them.

### Selecting columns

The `cut` command is used to extract sections of text from each line in a file.
By default, it selects 1-indexed columns (`-f`) a tab-delimited file.

```
$ cut -f 1 fileA.bed
```

It can also select an inclusive range of columns

```
$ cut -f 2-3 fileA.bed
```

or even characters.

```
$ cut -c 2-10 fileA.bed
```

For instances when you are not working with tabs, you can also specify the character to split on.
This is often useful when processing GFF3 files.

```
$ cut -d ';' -f 2 ecoli.gff3
```

You can also find more information on the man page or [on Wikipedia](https://en.wikipedia.org/wiki/Cut_(Unix)).

### Selecting words

The `grep` is a very useful utility to **G**lobally search a **R**egular **E**xpression and **P**rint it.
The most basic function is to see if a file contains a specific word or sequence.
We can start by searching for same sequence (`TCCAACTTATTGATAGTGTTTTATGTTCAGATAATGCCGATG`) we did with less.

```
$ grep "TCCAACTTATTGATAGTGTTTTATGTTCAGATAATGCCGATG" ecoli.fasta
```

We can also use `grep` to select all the exons from the ecoli annoation.

```
$ grep "exon" ecoli.gff3
```

By default grep looks for the string or regular expression inside the parentheses and prints the entire line that contains it.
Using the `-o` argument, we can choose to print only the matching string. 

```
$ grep -o "TCCAACTTATTGATAGTGTTTTATGTTCAGATAATGCCGATG" ecoli.fasta
```

Grep is especially powerful when using [regular expressions](https://www.gnu.org/software/findutils/manual/html_node/find_html/grep-regular-expression-syntax.html) to match multiple cases.

| Expression | Matches |
|------------|:--------|
| `.` | Any character except newline |
| `\+` | One or more of the previous expression |
| `\*` | Zero or more of the previous expression |
| `\?` | Zero or at most one of the previous expression |
| `^` | Beginning of a line |
| `$` | End of a line |
| `[ expression ]` | A single character that matches any value inside the brackets |
| `[^ expression ]` | A single character that does not match any value inside the brackets |

Like we used `cut` to pull out some metadata from `ecoli.gff3`, we can use grep to find all the element names.

```
$ grep -o "Name=[^;]\+" ecoli.gff3
```

In this case we use the square brackets to match any character that is not a semi-colon one or more times.
You can also use the `-v` argument to find lines that do not match the regex.

```
$ grep -v "exon" ecoli.gff3
```

There is always something new to learn with `grep`, so I suggest reading the man page.

### Selecting unique information

The `uniq` (unique) command is very powerful, but we are only going to introduce it here.
It will become extremely useful during the next section after we learn to chain commands together.
`uniq` will take a file or an input and print out a single line of sequential duplicate lines.

```
$ head fileA.bed
```

Notice that the first two lines are duplicates of each other.


```
$ uniq fileA.bed
```

Printing the file with `uniq` removed all sequential duplicate regions from this bed file.
If you read the man page, you will also see that `uniq` can also print the number of occurrences

```
$ uniq -c fileA.bed
```

and only print lines that are duplicated.

```
$ uniq -d fileA.bed
```

## Exercises
- Print out the sequence depth column of a bedgraph file
- Find all genes in `ecoli.gff3`
- Print all the unique chromosomes in a bed file

## Topics Covered

* [&#9989; - Introduction](gnu_utils_01.md)
* [&#9989; - Viewing Files](gnu_utils_02.md)
* &#9989; - Filtering Files
* [**Next - Manipulating Files**](gnu_utils_04.md)
