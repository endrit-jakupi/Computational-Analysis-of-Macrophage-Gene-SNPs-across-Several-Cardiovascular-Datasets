# Computational Analysis of PF4 SNPs across Several Cardiovascular Datasets: A Comparative Study

## Project Overview

This project focuses on the computational analysis of genetic variants (SNPs) in and around the **PF4 gene** and their association with cardiovascular phenotypes such as heart failure, coronary artery disease, and myocardial infarction.

The goal is to build a reproducible data pipeline that:
- identifies SNPs located in the PF4 genomic region,
- retrieves their association statistics from large GWAS datasets,
- and organizes the results into structured representations for downstream analysis.

The pipeline integrates multiple public data sources, including Ensembl, NCBI dbSNP, GWAS Catalog, HERMES, and CARDIoGRAMplusC4D.

---

## 1. Create required folder structure

Inside the project root, create the following directories:

```bash
mkdir -p data/raw/hermes
mkdir -p data/raw/cardiogram_c4d
mkdir -p data/raw/finngen
```
## 2. HERMES (Heart Failure)

Download the summary statistics (excluding UK Biobank samples) from [here](https://www.kp4cd.org/node/283) and place the file as:

data/raw/hermes/hermes_hf.tsv

---

## 3. CARDIoGRAMplusC4D (CAD and MI)

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