# Next-Generation Sequencing (NGS) Analysis: WGS and RNA-Seq Workflow

## 🚀 Project Highlights
- Performed Whole Genome Sequencing (WGS) analysis including alignment and variant calling
- Conducted RNA-Seq analysis using Trinity for transcriptome assembly
- Generated visualization plots including PCA, volcano plot, and R plots
- Implemented end-to-end NGS pipeline using command-line tools

## 🧬 Overview
This project focuses on Next-Generation Sequencing (NGS) workflows including Whole Genome Sequencing (WGS) and RNA Sequencing (RNA-Seq). The study involves raw data processing, alignment, variant calling, transcriptome assembly, and visualization of gene expression patterns.

---

## 🧪 Tools Used
- FastQC  
- Trimmomatic  
- BWA  
- SAMtools  
- BCFtools  
- VCFtools  
- Trinity  
- R  


---

## ⚙️ Workflow

### 🔹 1. Data Retrieval
- Downloaded FASTQ files from NCBI SRA database using SRA Toolkit

---

## 🧬 Whole Genome Sequencing (WGS)

### 🔹 Alignment and Variant Calling

bwa index REFERENCE.fasta

bwa mem REFERENCE.fasta SRR29019342_1.fastq SRR29019342_2.fastq > out.sam

samtools flagstat out.sam > out-flagstat_output.txt

samtools view -S -b out.sam > out.bam
samtools sort out.bam -o out_sort.bam
samtools index out_sort.bam

samtools mpileup -f REFERENCE.fasta out_sort.bam > out.pileup

bcftools mpileup -f REFERENCE.fasta out_sort.bam | \
bcftools call -mv -Oz -o out.vcf.gz

bcftools index out.vcf.gz

vcftools --gzvcf out.vcf.gz \
--recode --recode-INFO-all \
--out out_filtered --minQ 30

conda create -n trinity_env -c bioconda -c conda-forge trinity
conda activate trinity_env

### RNA Sequencing (RNA-Seq)
Transcriptome Assembly (Trinity)

Trinity --version

Trinity --seqType fq \
--left SRR21159790_1_paired.fastq \
--right SRR21159790_2_paired.fastq \
--max_memory 50G \
--CPU 8 \
--output trinity_out_SRR21159790

By using the trinity output file can plot the R plot, PCA plot and volcano plot

## Author
Harini R
