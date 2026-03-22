# Next-Generation Sequencing (NGS) Analysis: WGS and RNA-Seq Workflow
## 🚀 Key Result
Identified genetic variants through whole genome sequencing and significant gene expression changes using RNA-Seq, supported by PCA clustering and volcano plot analysis.

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
The following workflow represents the complete NGS pipeline implemented for genome and transcriptome analysis.
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

## 📊 Results Visualization

### PCA Plot
![PCA](pca.png)

*PCA plot showing clustering of samples based on gene expression patterns*

### Volcano Plot
![Volcano](volcano.png)

*Volcano plot showing significantly upregulated and downregulated genes*

### R Plot
![Rplot](rplot.png)

*R plot representing overall gene expression distribution across samples*

## 🧠 Interpretation

- PCA plots showed clear clustering of samples, indicating variation between experimental conditions  
- Volcano plots highlighted significantly upregulated and downregulated genes  
- R plots demonstrated overall gene expression distribution  

## 🧠 Key Findings
- Identified significant gene expression changes across samples  
- Visualization revealed patterns useful for biological interpretation  
- Differential expression analysis helped identify potential genes of interest  

## 📌 Conclusion
This study demonstrates how statistical analysis and visualization techniques can be used to interpret gene expression data and identify biologically significant patterns.
