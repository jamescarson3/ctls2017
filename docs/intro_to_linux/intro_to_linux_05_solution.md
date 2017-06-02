
1) How large is `Homo_sapiens.GRCh38.dna.chromosome.21.fa` before and after compression?
```
$ cd 
$ cd IntroToLinuxHPC/Lab02
$ ls -l Homo_sapiens.GRCh38.dna.chromosome.21.fa
  # 42384874 bytes before compression
$ gzip -v Homo_sapiens.GRCh38.dna.chromosome.21.fa.gz
  # 11772051 bytes after compression
```

2) How large is `websters.txt` before and after compression?
```
$ cd 
$ cd IntroToLinuxHPC/Lab01
$ ls -l websters.txt
  # 2493109 bytes before compression
$ gzip -v websters.txt
  # 754559
```

3) Assuming the same compression rate, how large will 1 TB of text files be after compression?

The fasta file is 27.8% of the original size, and the dictionary is 30.2% of the original size. Assuming these numbers are about average for raw text files, a 1 TB file would reduce down to ~**290 GB**.


[Return](intro_to_linux_05.md)

