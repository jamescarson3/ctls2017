TMP = GCF_001420955.1_ASM142095v1_genomic.fna.gz GCF_001420955.1_ASM142095v1_genomic.gff.gz
TARGETS = ecoli.fasta.bwt ecoli.gff3 SRR2014925.bam
NCORES = $(shell getconf _NPROCESSORS_ONLN)

all: check $(TARGETS)
	rm -rf $(TMP)

%.gz:
	wget ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/001/420/955/GCF_001420955.1_ASM142095v1/$@
	
ecoli.fasta: GCF_001420955.1_ASM142095v1_genomic.fna.gz
	gzip -dc $^ > $@

ecoli.fasta.%: ecoli.fasta
	bwa index $^

ecoli.gff3: GCF_001420955.1_ASM142095v1_genomic.gff.gz
	gzip -dc $^ > $@

SRR2014925_%.fastq:
	fastq-dump --split-files SRR2014925

SRR2014925.sam: ecoli.fasta SRR2014925_1.fastq SRR2014925_2.fastq
	bwa mem -t $(NCORES) $^ > $@

SRR2014925.bam: SRR2014925.sam
	samtools view -bS -@ $(NCORES) $^ > $@

clean:
	rm -rf $(TMP) $(TARGETS) ecoli* SRR*

check: FQD-exists
FQD-exists:
	@which fastq-dump > /dev/null
