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

---

## 5. Notebook Execution Order

### Main PF4 Cardiovascular Association Analysis

The main PF4 cardiovascular association analysis pipeline should be executed in the following order:

1. `ensembl_region.ipynb`  
   Retrieve the PF4 genomic coordinates and define the PF4 ±50 kb genomic region.

2. `gwas_catalog.ipynb`  
   Retrieve PF4-related SNP–trait associations from the GWAS Catalog API.

3. `hermes.ipynb`  
   Retrieve PF4-region associations from the HERMES HF summary statistics excluding UK Biobank samples.

4. `hermes_ukb.ipynb` *(complementary analysis)*  
   Retrieve PF4-region associations from the HERMES HF summary statistics including UK Biobank samples.

5. `cardiogram_c4d.ipynb`  
   Retrieve PF4-region associations from the CARDIoGRAMplusC4D CAD and MI datasets.

6. `finngen_replication.ipynb`  
   Perform independent replication analyses using FinnGen HF, CAD, and MI datasets.

7. `results.ipynb`  
   Combine the retrieved association results into the final `pf4_cardiovascular_associations.csv` table.

---

### Complementary PF4 NCBI dbSNP Analysis

The following notebook performs the complementary extraction and annotation of PF4 variants from NCBI dbSNP:

1. `ncbi_variants.ipynb`  
   Extract and annotate PF4-related variants together with frequency and positional annotations into the final `pf4_variants.csv` table.

---

### Quality-Control Summary

The following notebook generates a quality-control summary for the final PF4 cardiovascular association and variant datasets:

1. `qc_summary.ipynb`  
   Perform quality-control checks across the final association and variant tables and generate the final `pf4_qc_summary.csv` summary table.