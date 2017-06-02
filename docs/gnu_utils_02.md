# Viewing Text Files

In this section, we will learn to view text files using

- `cat`
- `head`
- `tail`
- `less`

While "text files" may not sound exciting, most bioinformatics data formats are simple text files.
We will be using actual data files pulled from [NCBI](https://www.ncbi.nlm.nih.gov/) in our exercises, so a basic understanding will be beneficial.

## Data Formats

We will initially focus on these four data formats. More types can be found on the [UCSC genome site](https://genome.ucsc.edu/FAQ/FAQformat.html).

### FASTA

A "FASTA file" is a text-based file with the `.fa` or `.fasta` extension that represents sequences of nucleotides using single-letter codes. The basic format is as follows:

1. A header line beginning with `>`
2. Any number of lines of sequence characters. Usually
  * A - Adenine
  * G - Guanine
  * C - Cytosine
  * T - Thymine
  * N - Unknown Base

An example FASTA could look like

```
>Sequence1
AAGGTTCC
>Sequence2
AAAAAAAAAAAAA
AAAAAAAAAAAAA
AAAAAAAAAAAAA
```

There cannot be extra lines in this file. More information can be found [on the Wikipedia page](https://en.wikipedia.org/wiki/FASTA_format).

### FASTQ

The "FASTQ" format is similar to "FASTA" except it was specifically designed for shorter sequences and certainty (quality) scores.
These files have a `.fq` or `.fastq` extension and contain four lines per **read**:

1. Header beginning with `@` containing a unique name
2. Actual sequence with FASTA coding
3. Second header beginning with `+` (does not need any content)
4. Character encoded quality scores

Two reads in an example FASTQ could look like

```
@SRR2014925.235
GATCACAGAAGAAGCCAGTTCGATTTGTTGAGCGCGTAATGACGCGAGATCCATAATCGC
+
>3>AAFFFFFFFCGGCGGGGGGHHHEHDGGHHHGGGGGGGHHHGGGGGGGHHHHHHHHGG
@SRR2014925.236
GTGGTAATGCGCAAGCTGAAAGATTAATTCGGAGTAGGTCGGATAAGACGCGCCAGCGCC
+
3AAAAFFFFFBAEG?GGGGGGGCGHGHHHHGHGGGHHGHGGGGGGHHHHEGGGGGGGGGG
```

Notice that the second header line can be empty, and the quality scores are on the Phred+33 scale default for (`fastq-dump`), where the characters correspond the following values.
This allows a single character represent a two-digit number.

```
Characters   !"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHI
             |                         |    |        |
Values       0........................26...31.......40
```

### BED

One of the most versatile bioinformatics formats is the "BED" (Browser Extensible Data) format, which is used to describe regions of a FASTA sequence.
At a minimum, each line of a BED file must have three columns separated by tabs:

1. Chromosome (sequence)
2. Start position (0-indexed)
3. Ending position (not-inclusive meaning [0,5) for first 5)

An example BED file that corresponded to our example FASTA could be

```
Sequence1	0	4
Sequence1	4	8
```

which would select the following regions

```
Sequence1    AAGGTTCC
Index        012345678
BED1         AAGG)
BED2             TTCC)
```

Where the `)` index is excluded and serves as the ending boundary.
More columns can also be added to this format to represent sequencing depth, reference strand, and [more](https://genome.ucsc.edu/FAQ/FAQformat.html#format1)

### GFF3

GFF3 files (`.gff`, `.gff3`) are tab-delimited like BED file, but are 1-indexed and contain 9 columns by default.
They are also meant to refer to other regions instead of being independent of each other, making them ideal to annotate genomes with transcripts, gene-models, exons, and more.
Each line of a GFF3 file contains the following columns

1. Chromosome (sequence)
2. Source (program or machine)
3. Feature Type {exon, gene, mRNA, ...}
4. Start (1-indexed)
5. End (1-indexed and inclusive)
6. Score (float or `.` for nothing)
7. Strand (`+` or `-`)
8. Coding phase (0, 1, 2, or `.` for NA)
9. Attributes (key-value pairs separated by semicolons)

An example GFF3 could look like

```
##gff-version 3
Sequence1	.	gene	1	4	.	+	.	ID=region01
Sequence1	.	gene	5	8	.	+	.	ID=region02
```

Header sequences are prefixed by `#` characters. More information about the GFF3 format can be found [here](http://www.ensembl.org/info/website/upload/gff3.html).

## Viewing Files

Now that you have a basic understanding of these file formats, lets learn to view them. We first need some files to work with, so lets download some data I pre-formatted.

```
wget https://raw.githubusercontent.com/jamescarson3/ctls2017/master/docs/gnu_utils/Makefile
module load bedtools sratoolkit
make all
```

### Printing a whole file

When necessary, you can print an entire file with the `cat` command.
The `cat` command reads input sequentially and writes the contents to the standard output.
This is great to quickly print an entire file.

```
$ cat fileA.bed
```

You will quickly learn that `cat` can sometimes be overwhelming when files are huge.

```
$ cat SRR2014925_1.fastq
```

For big files like this, you can either wait for it to finish printing or hit `ctrl+C` to kill the program.

`cat`, which is named for concatenate, can also be used to print multiple files in \[sequential\] order.

```
$ cat fileA.bed fileB.bed
```

Notice that files are printed in the order you specify on the command line.

```
$ cat fileB.bed fileA.bed
```

You can also use [wildcards](http://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm) to represent multiple files.

```
$ cat file[AB].bed
$ cat file*.bed
$ cat file*
$ cat *bed
```

If you try all of the above commands, you will notice that they all resolve to the same output.

### Printing part of a file

For times when the whole file is too much information, you can print the first few lines using the `head` command.

```
$ head fileA.bed
```

If you are only interested in the end of a file, the `tail` command will print the last few lines of a file.

```
$ tail fileA.bed
```

If you specify multiple files at once, head will automatically prepend the filename before the selected lines.
`cat` does not do this because it was specifically designed to concatenate file contents without extra artefacts.

```
$ cat file*.bed
$ head file*.bed
```

You can also specify the number of lines you wish to print with the `-n` argument.

```
$ head -n 2 fileA.bed
$ tail -n 2 fileA.bed
```

#### Explore

* How many lines get printed by default?
* What happens when you file has fewer lines?
* Find other useful parameters by looking at the documentation (`man head`).

### Browsing through a file

Instead of printing an entire file, or a specific part of a file, you can also browse though it with the `less` command.
`less` does not automatically exit like `cat` and `head`, so lets take a quick look at the [documentation](https://en.wikipedia.org/wiki/Less_(Unix)) and some important commands.

| Key | Description |
|-----|---------|
|Q|Quit|
|&uarr; &darr;|Move up or down a line|
|&larr; &rarr;|Scroll left or right|
|space bar|Scroll down a "page"|
|B|Scroll up a "page"|

Try using it on fileA.bed

```
$ less fileA.txt
```

The whole file should be visible in a single terminal, so you should be unable to scroll.
Try using it on the *E. coli* annotation file.

```
$ less ecoli.gff3
```

You can also search for specific patterns with `less`.

| Key | Description |
|-----|---------|
| `/<text>` | Search for `<text>` in the file |
| N | Next match |
| shift+N | Previous match |

Try to find "exon" and "gene" regions in `ecoli.gff3`.

The more you use less, the more you will appreciate less. `:D`

#### Explore

* Try searching for a regular expression
* Use less on a "SAM" file with and without the `-S` argument

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
- What chromosome in `ecoli.fasta` contains `TCCAACTTATTGATAGTGTTTTATGTTCAGATAATGCCGATG`?
<br>

[Back - Introduction](gnu_utils_01.md) &nbsp;&nbsp;&nbsp; [Next - Filtering Files](gnu_utils_03.md)
