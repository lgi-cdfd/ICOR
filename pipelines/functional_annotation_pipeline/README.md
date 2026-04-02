# Functional Annotation Pipeline

## Overview

Performs comprehensive protein annotation integrating similarity search and domain analysis.

---

## Step 1: DIAMOND BLASTP

```
diamond blastp \
-d nr \
-q proteins.fasta \
-o blast.xml \
-f 5 \
-p 40
```

---

## Step 2: InterProScan

```
interproscan.sh \
-i proteins.fasta \
-o interpro.xml \
-f XML \
-cpu 40
```

---

## Step 3: EggNOG Mapper

```
emapper.py \
-i proteins.fasta \
--output proteins \
--output_dir . \
--data_dir data \
--cpu 80
```

---

## Step 4: Integration

* Combine BLAST + InterProScan + EggNOG outputs
* Generate GO & KEGG mappings
* Export OmicsBox-compatible files

---

## Output

* Functional annotations
* GO terms
* KEGG pathways

