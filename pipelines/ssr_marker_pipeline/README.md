# SSR Marker Pipeline

## Overview

Pipeline for identification and validation of SSR markers and primer specificity.

---

## Step 1: SSR Detection (KRAIT)

Run KRAIT for SSR identification and primer design.

---

## Step 2: BLAST Database Creation

```
makeblastdb -in genome.fa -dbtype nucl -out db
```

---

## Step 3: Primer Specificity Check

```
blastn -task blastn-short \
-query primers.fa \
-db db \
-out blast_results.txt
```

---

## Step 4: MFEprimer Analysis

### Index genome

```
mfeprimer index -i genome.fa
```

### Specificity

```
mfeprimer spec \
-i primers.fa \
-d genome.fa \
--minSize 80 \
--maxSize 300
```

### Dimer formation

```
mfeprimer dimer -i primers.fa
```

### Hairpin structures

```
mfeprimer hairpin -i primers.fa
```

---

## Output

* Validated SSR markers
* High-specificity primers

