# Computational Analysis of Macrophage-Associated Genetic Variants Across Several Cardiovascular GWAS Datasets

## Project Overview

This project focuses on the computational analysis of genetic variants (SNPs) in 
and around a set of macrophage-related genes and their association with 
cardiovascular phenotypes such as heart failure, coronary artery disease, and 
myocardial infarction.

The goal is to build a reproducible data pipeline that:
- identifies SNPs located in the queried gene regions,
- retrieves their association statistics from large GWAS datasets,
- and organizes the results into structured representations for downstream analysis.

---

## 1. Create required folder structure

Inside the project root, create the following directories:

```bash
mkdir -p data/raw/hermes
mkdir -p data/raw/cardiogram_c4d
mkdir -p data/raw/finngen
```

## 2. HERMES (Heart Failure)

Download the Heart Failure (HF) summary statistics (excluding UK Biobank samples) 
from [here](https://www.kp4cd.org/node/283) and place the file as:
data/raw/hermes/hermes_hf.tsv

---

## 3. CARDIoGRAMplusC4D (Coronary Artery Disease and Myocardial Infarction)

Download the harmonized GWAS summary statistics for:

- Coronary artery disease (CAD) from [here](https://ftp.ebi.ac.uk/pub/databases/gwas/summary_statistics/GCST003001-GCST004000/GCST003116/)
- Myocardial infarction (MI) from [here](https://ftp.ebi.ac.uk/pub/databases/gwas/summary_statistics/GCST011001-GCST012000/GCST011365/)

and place them as:

data/raw/cardiogram_c4d/cardiogram_cad_harmonized.tsv
data/raw/cardiogram_c4d/cardiogram_mi_harmonized.tsv

---

## 4. FinnGen (Replication)

FinnGen is used as an independent replication resource.

Access the data from [here](https://www.finngen.fi/en/access_results) or download the required datasets directly:

- I9_HEARTFAIL (Heart failure, strict) - download [here](https://storage.googleapis.com/finngen-public-data-r12/summary_stats/release/finngen_R12_I9_HEARTFAIL.gz)
- I9_CHD (Major coronary heart disease event) - download [here](https://storage.googleapis.com/finngen-public-data-r12/summary_stats/release/finngen_R12_I9_CHD.gz)
- I9_MI_STRICT (Myocardial infarction, strict) - download [here](https://storage.googleapis.com/finngen-public-data-r12/summary_stats/release/finngen_R12_I9_MI_STRICT.gz)

Place the files as:

data/raw/finngen/finngen_hf.tsv
data/raw/finngen/finngen_cad.tsv
data/raw/finngen/finngen_mi.tsv

---

## 5. Notebook Execution Order

1. `01_gene_regions.ipynb`  
   Retrieve genomic coordinates and define query regions for all genes in the gene list.

2. `02_gwas_catalog.ipynb`  
   Retrieve SNP–trait associations for all gene regions from the GWAS Catalog API.

3. `03_hermes.ipynb`  
   Extract gene-region associations from the HERMES heart failure summary statistics.

4. `04_cardiogram_c4d.ipynb`  
   Extract gene-region associations from the CARDIoGRAMplusC4D CAD and MI summary statistics.

5. `05_finngen.ipynb`  
   Extract gene-region associations from the FinnGen HF, CAD, and MI summary statistics for independent replication.

6. `06_cardiovascular_associations.ipynb`  
   Combine all association results into the final `cardiovascular_associations.csv` table.

7. `07_gnomad.ipynb`  
   Retrieve gnomAD variant frequency data for all gene regions and classify variants by allele-frequency thresholds.

8. `08_qc_summary.ipynb`  
   Perform quality-control checks across the cardiovascular association table and 
   the gnomAD variant frequency table, and generate the `qc_summary.xlsx` summary.

9. `09_prioritized_variants.ipynb`  
   Merge the cardiovascular association table with the gnomAD variant frequency 
   annotations to produce the `prioritized_variants.csv`, `hf_prioritized_variants.csv`, 
   and `top_variants_per_gene.csv` tables.

10. `10_summary_tables.ipynb`  
    Compute gene-level association counts, significance tier distributions, and 
    functional consequence breakdowns across all candidate genes and save the 
    results to `summary_tables.xlsx`.