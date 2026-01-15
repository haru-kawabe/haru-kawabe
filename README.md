# Bioinformatics Portfolio

Hi there 👋

I work on bioinformatics analysis pipelines,
especially for long-read sequencing and variant calling.
This repository showcases workflows and scripts I have developed for genomic data analysis.

---

## 📌 Featured Project

**[bioinformatics](https://github.com/haru-kawabe/bioinformatics)**  
A complete pipeline for long-read variant analysis and VCF filtering.

---

## 🛠 Tools & Skills

- Linux / Bash scripting
- Long-read mapping: minimap2
- BAM processing: samtools
- Variant calling & filtering: bcftools
- RNA-seq alignment: STAR / HISAT2
- Workflow automation using shell scripts
- Reproducible pipelines

---

## ⚡ Example Commands

```bash
# Map short or long reads to reference genome
minimap2 -ax map-ont ref.fasta reads.fastq | samtools sort -o aln.bam
bowtie2 --very-sensitive -k 1 -p 8 -x ref_bt2 -1 Read1.fastq.gz -2 Read2.fastq.gz 2> bowtie2.log | samtools view -@ 8 -b -f 2 -q 30 | -o .bam

# Call variants
bcftools mpileup -f ref.fasta aln.bam | bcftools call -mv -Oz -o variants.vcf.gz

# Filter VCF by quality and depth
bcftools filter -i 'MQ>40 && DP>20 && INFO/ALT_FREQ>0.8' variants.vcf.gz -Oz -o filtered.vcf.gz
