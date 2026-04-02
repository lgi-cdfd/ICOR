# Functional Enrichment Pipeline

## Overview

Performs transcript quantification followed by differential expression and enrichment analysis.

---

## Step 1: Indexing

```
salmon index -t Ref.fasta -i Ref
```

---

## Step 2: Quantification

```
salmon quant \
-i Ref \
-l A \
-1 Read_1.fastq.gz \
-2 Read_2.fastq.gz \
-p 23 \
--validateMappings
```

---

## Step 3: Differential Expression

Performed in R using tximport and DESeq2.

---

## Step 4: Functional Enrichment

* Gene Ontology (GO)
* KEGG pathway analysis
  
---

## Output

* DEG tables
* GO enrichment plots
* KEGG pathway maps

