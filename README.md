# ICOR: Integrated Computational Omics Resource

## Overview

ICOR is a comprehensive computational framework designed for large-scale transcriptomic analysis, integrating multiple pipelines for:

* lncRNA prediction
* SSR marker discovery and validation
* Functional enrichment analysis
* Functional annotation

The framework ensures reproducibility, modularity, and standardized reporting across analyses.

---

## Pipelines Included

### 1. Transcriptome Assembly Pipeline

Performs preprocessing and de novo assembly of RNA-Seq data to generate a high-quality non-redundant unigene dataset for downstream analyses:

* Quality assessment using FastQC
* Adapter trimming and filtering using Trimmomatic
* De novo transcriptome assembly using Trinity
* Redundancy reduction using CD-HIT-EST

This pipeline serves as the foundational step, providing assembled transcripts that are subsequently used for lncRNA prediction, SSR marker identification, functional annotation, and enrichment analyses.

### 2. lncRNA Prediction Pipeline

Integrates multiple tools for high-confidence identification of long non-coding RNAs:

* CPC2
* PLEK
* CNCI
* CPAT

---

### 3. SSR Marker Pipeline

Pipeline for identification and validation of microsatellite markers:

* KRAIT
* BLAST specificity filtering
* MFEprimer validation

---

### 4. Functional Enrichment Pipeline

Transcript-level quantification and downstream enrichment:

* Salmon (quantification)
* Differential expression (R-based)
* GO and KEGG enrichment

---

### 5. Functional Annotation Pipeline

Comprehensive protein annotation:

* DIAMOND BLASTP
* InterProScan
* EggNOG mapper
* OmicsBox integration

---

## License

MIT License

