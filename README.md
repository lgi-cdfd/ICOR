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

### 1. lncRNA Prediction Pipeline

Integrates multiple tools for high-confidence identification of long non-coding RNAs:

* CPC2
* PLEK
* CNCI
* CPAT

---

### 2. SSR Marker Pipeline

Pipeline for identification and validation of microsatellite markers:

* KRAIT
* BLAST specificity filtering
* MFEprimer validation

---

### 3. Functional Enrichment Pipeline

Transcript-level quantification and downstream enrichment:

* Salmon (quantification)
* Differential expression (R-based)
* GO and KEGG enrichment

---

### 4. Functional Annotation Pipeline

Comprehensive protein annotation:

* DIAMOND BLASTP
* InterProScan
* EggNOG mapper
* OmicsBox integration

---

## License

MIT License

