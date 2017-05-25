# Life Sciences Workflow 2
### Course objectives
The main objective of this course is to demonstrate how a bioinformatics workflow can be seamlessly run using TACC resources from raw input to biological interpretation. In particular, transcriptome analysis will be demoed as it is a familiar concept among wide range of disciplines. 

### 1. Transcriptome analysis
Transcriptome is simply defined as all of RNA molecules in a single cell. This represents expression levels of all genes for a single condition of cell for a specie at given time. It is also referred as expression profiling. Transcriptome analysis unlike Genome analysis can show differences in the exact same cell that are in different external environment. 

#### a. Examples from high-impact journal
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image1.png)
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image2.png)
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image3.png)

#### b. Scientific background
The pipeline uses Next-generation sequencing data to as a raw input. 

### 2. Transcriptome analysis workflow using TopHat suite
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image4.jpg)

### 3. Where to find required test-dataset
https://www.ncbi.nlm.nih.gov/sra/SRX2771645

https://www.ncbi.nlm.nih.gov/sra/SRX2771647

### 4. Tools used in this session
Tuxedo suite 
includes: TopHat, Cufflinks, Cuffmerge, Cuffdiff
Samtools
### 5. Benchmarking analysis (TopHat)
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image5.png)
### 6. Information on test dataset (Scientific background)
### 7. TopHat and Cufflink demo/hands-on
### 8. Functional analysis with BARtools
### 9. Hands-on using Samtools 
```module load samtools
samtools flagstat test.sam
```
