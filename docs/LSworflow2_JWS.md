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
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image7.png)

### 3. Where to find required test-dataset
https://www.ncbi.nlm.nih.gov/sra/SRX2771645

https://www.ncbi.nlm.nih.gov/sra/SRX2771647

* Hands-on: How do we download these files?
### 4. Tools used in this session
Tuxedo suite 
includes: TopHat, Cufflinks, Cuffmerge, Cuffdiff
Samtools

### 5. Benchmarking analysis (TopHat)
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image5.png)

### 6. Information on test dataset (Scientific background)
The two sequencing files are of a plant model organism, *Arabidopsis Thaliana*. A member of the Brassica family, Arabidopsis thaliana is a favorite research subject for plant molecular geneticists because of its remarkably small genome size (about 100,000 kB, with less than 25% repetitive sequences), ease of culture in the lab, short stature and life cycle, and amenability to genetic mapping studies and other techniques (such as transformation and gene cloning).

The first of the files is from Col-0 strain, which is columbia seed. A widely used wild type seed, selected for its high fertility, vigor, and responsiveness to changes in photoperiod. Contains no visible genetic markers. 

Second is of jazQ mutant, which has 
### 7. TopHat and Cufflink demo/hands-on

```
module load perl bowtie tophat
```
What happens if you do just `module load tophat` without prerequisite modules?

### 8. Alignment statistics
``` 
module load samtools
samtools flagstat input.sam
```

### 9. Functional analysis with BARtools
http://bar.utoronto.ca/ntools/cgi-bin/ntools_classification_superviewer.cgi
Using the dataset you got from running cuffdiff, you should be able to extract top 100 genes with highest log-fold changes in expression. Save the names of these genes as a separate text file, and copy the names of genes to the tool above. What functional enrichment do you see in mutant strain?
```
sort -nrk 12 gene_exp.diff > gene_exp.diff.sort
head -100 gene_exp.diff.sort > gene_exp.diff.sort.top100
cut -f 3 gene_exp.diff.sort.top100 > gene_exp.diff.sort.top100.names
```
![Alt text](https://raw.githubusercontent.com/wonaya/test/master/image6.png)

Removal of multiple JAZ genes in this jaz quintuple (jazQ) mutant led to constitutive activation of JA responses, causing hypersensitivity to exogenous JA treatment, upregulation of defense-related genes, increased production of secondary metabolites and higher resistance to insect herbivory attack *Campos et al. Nat. Comms. 2016* https://www.ncbi.nlm.nih.gov/pubmed/27573094

#### Congratulations, You can now do Transcriptome analysis!
