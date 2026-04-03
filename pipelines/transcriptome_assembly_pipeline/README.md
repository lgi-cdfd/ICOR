# Transcriptome Assembly Pipeline

## Overview

This pipeline performs quality control, preprocessing, de novo transcriptome assembly, and redundancy reduction to generate a high-quality non-redundant unigene dataset suitable for downstream analyses.

---

## Input

* Raw paired-end RNA-Seq reads (`*.fastq.gz`)

---

## Step 1: Quality Assessment (FastQC)

Raw sequencing reads were evaluated to assess per-base quality, GC content, adapter contamination, and sequence duplication levels.

```bash
mkdir fastqc_reports

fastqc \
raw/*.fastq.gz \
-o fastqc_reports \
-t 20
```

---

## Step 2: Read Pre-processing (Trimmomatic)

Adapter trimming and quality filtering were performed using the following parameters:

* ILLUMINACLIP: TruSeq3-PE.fa:2:30:10
* LEADING: 3
* TRAILING: 3
* SLIDINGWINDOW: 4:15
* MINLEN: 32

Only high-quality paired reads were retained for downstream analysis.

```bash
mkdir -p trimmed_reads

trimmomatic PE -threads 20 \
raw/Read_1.fastq.gz raw/Read_2.fastq.gz \
trimmed_reads/paired_1.fastq.gz \
trimmed_reads/unpaired_1.fastq.gz \
trimmed_reads/paired_2.fastq.gz \
trimmed_reads/unpaired_2.fastq.gz \
ILLUMINACLIP:TruSeq3-PE.fa:2:30:10 \
LEADING:3 \
TRAILING:3 \
SLIDINGWINDOW:4:15 \
MINLEN:32
```

---

## Step 3: Post-trimming Quality Check (Optional but Recommended)

```bash
mkdir -p fastqc_trimmed

fastqc \
trimmed_reads/*.fastq.gz \
-o fastqc_trimmed \
-t 20
```

---

## Step 4: De novo Transcriptome Assembly (Trinity)

High-quality paired-end reads were assembled using Trinity to maximize transcript diversity.

```bash
mkdir -p trinity_assembly

Trinity \
--seqType fq \
--left trimmed_reads/paired_1.fastq.gz \
--right trimmed_reads/paired_2.fastq.gz \
--SS_lib_type RF \
--min_contig_length 200 \
--CPU 64 \
--max_memory 500G \
--output trinity_assembly
```

---

## Step 5: Redundancy Reduction (CD-HIT-EST)

To remove redundant transcripts and overlapping isoforms, clustering was performed at 90% sequence identity.

```bash
mkdir -p cdhit_output

cd-hit-est \
-i trinity_assembly/Trinity.fasta \
-o cdhit_output/unigenes.fasta \
-c 0.90 \
-n 8 \
-T 40 \
-M 0
```

---

## Output

* `Trinity.fasta` → raw transcript assembly
* `unigenes.fasta` → non-redundant transcript set

---

## Notes

* Ensure sufficient RAM (≥500 GB recommended) for Trinity execution
* Verify strand-specific library type before running (`RF` used here)
* Output unigenes serve as input for downstream pipelines (lncRNA prediction, SSR analysis, annotation, enrichment)

