# Redirecting and Piping Output

Now that you can view and filter files, it would be good to save that information without copying and pasting the text from your terminal.
Luckily, Linux employs [redirection](https://en.wikipedia.org/wiki/Redirection_(computing)) for communication between processes and writing to files.
In this section, we will explore the following commands

- `>` - stdout
- `>>` - append
- `<` - stdin
- `|` - pipe

We will again be using the data you generated for viewing files.
If you no longer have these files, plese [go back](gnu_utils_02.md) and regenerate them.

### Redirecting Output

When the `>` character is placed at the end of a command, it instructs the shell to write the ouput into a file instead of printing it to your terminal.

```
$ head -n 8 SRR2014925_1.fastq > two_reads.fastq
```

You can then use `cat` or `head` to see the output of the new file `two_reads.fastq`.

```
$ ls *fastq
$ cat two_reads.fastq
```

This is especially useful when dealing with large outputs

```
$ head -n 400000 SRR2014925_1.fastq > 100k_reads.fastq
```

#### Explore

- Write all exons from `ecoli.gff3` to a file
- Write all SRR2014925 reads to a single file

### Appending Output

The `>>` command will do everything that `>` does, but instead of writing to the beginning of a file, it will append the text to an existing file.

```
$ cat fileA.bed > one.bed
$ cat fileB.bed > one.bed
$ cat one.bed

$ cat fileA.bed >> two.bed
$ cat fileB.bed >> two.bed
$ cat two.bed
```

This command is useful when you want to combine the output from multiple commands into a single file.
Just remember that `>>` will append to any existing files, so you may have to delete your output file between runs.

```
$ head -n 4 SRR2014925_1.fastq >> one.bed
$ cat one.bed
```

Your scripts should either delete the old file

```
$ rm one.bed
$ head -n 4 SRR2014925_1.fastq >> one.bed
```

or not use append the first time.

```
$ head -n 4 SRR2014925_1.fastq > one.bed
$ head -n 4 SRR2014925_1.fastq >> one.bed
```

#### Explore

- Write the first two reads from both SRR2014925 fastq files to a single file
- Write all exons and gene records from `ecoli.gff3` to a single file

### Piping Output

Everyone that has interacted with bioinformatics has probably heard the term "pipeline" when reffering to scripts.
This term originates from creating scripts that chain multiple commands together with the `|` character.
The pipe is a form of redirection, but instead of writing the output to a file, it uses it as input to another program.
Right now, you can make a pipeline with temporary files.

```
$ grep "NZ_CP013024.1" ecoli.gff3 > NZ_CP013024.1.gff3
$ grep "exon" NZ_CP013024.1.gff3 > NZ_CP013024.1_exons.gff3
```

But pipes allow you to simplify your workflow down to

```
$ grep "NZ_CP013024.1" ecoli.gff3 | grep "exon" NZ_CP013024.1.gff3 > NZ_CP013024.1_exons.gff3
```

while also producing the same output.


In the last two sections, we have learned to view and filter files

Often times, you will want specific information from your files. This could be specific columns from a file or select information.

Two of the most versatile commands for bioinformatics files are

- `>/>>`
- `<`
- `|`

## Exercises
- Print out depth column of a bed file
- Find all exons in an annotation
- Print all the unique chromosomes in a bed file

<table width="100%" border="0"><tr>
<td align="left"><a href="gnu_utils_03.html">Filtering Files</a></td>
<td align="center">Redirection</td>
<td align="right"><a href="gnu_utils_05.html">Manipulating Files</a></td>
</tr></table>
