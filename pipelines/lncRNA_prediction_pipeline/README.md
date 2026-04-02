# lncRNA Prediction Pipeline

## Overview

This pipeline integrates four independent tools to identify high-confidence lncRNAs from transcript sequences.

---

## Input

* Transcript FASTA file: `Renamed_Ref_unigene.fasta`

---

## Step 1: CPC2

Modified CPC2 scripts (originally Python 2) to support Python ≥3.8.

```
python CPC2.py \
-i /path/Renamed_Ref_unigene.fasta \
-o /path/CPC2_output
```

---

## Step 2: PLEK

Installed from SourceForge and executed locally.

```
python PLEK.py \
-fasta Renamed_Ref_unigene.fasta \
-out PLEK_output \
-thread 20 \
-minlength 200 \
-isoutmsg 1 \
-isrmtempfile 1
```

---

## Step 3: CNCI (HPC Execution)

Environment: `cnci_env`

```
python CNCI.py \
-f Renamed_Ref_unigene.fasta \
-o CNCI_output \
-p 40 \
-m ve
```

---

## Step 4: CPAT

Environment: `cpat_env`

```
cpat \
-g Renamed_Ref_unigene.fasta \
-d Mus_musculus_logitModel.RData \
-x Mus_musculus_Hexamer.tsv \
-o CPAT_output \
--antisense
```

---

## Final Filtering Strategy

* Retain transcripts predicted as non-coding by ≥3 tools
* Remove transcripts <200 bp

---

## Output

* High-confidence lncRNA list
* Tool-specific prediction files

