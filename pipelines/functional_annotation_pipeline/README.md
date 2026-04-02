# Functional Annotation Pipeline

## Overview

Performs comprehensive protein annotation integrating similarity search and domain analysis.

---

## Step 1: DIAMOND BLASTP

```
diamond blastp \
-d nrdb.dmnd \
-q proteins.fasta \
-o blast.xml \
--outfmt 5 \
-threads 40
```

---

## Step 2: InterProScan

```
interproscan.sh \
-i proteins.fasta \
-goterms \
-f XML \
-o interpro.xml \
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

