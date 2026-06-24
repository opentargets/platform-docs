---
description: June 2026 version
---

# 🆕 Baseline expression

## Overview

Baseline (healthy, unstimulated) human RNA and protein expression data can help determine whether a target is expressed broadly across tissues and cell types or selectively in specific biological contexts. The presence of a target molecule in the tissue or cell type of interest is an important consideration throughout the drug discovery and development process.

The Open Targets Platform integrates baseline expression data generated using three complementary technologies:

* Single-cell RNA sequencing (scRNA-seq)
* Bulk RNA sequencing (RNA-seq)
* Mass spectrometry (MS)-based proteomics

Data are collected from four sources:

| **Data source**      | **Technology**               | **Coverage**                         |
| -------------------- | ---------------------------- | ------------------------------------ |
| **Tabula Sapiens**   | Single-cell RNA-seq          | 66 tissues, 180 annotated cell types |
| **GTEx (v10)**       | Bulk RNA-seq                 | 54 tissues                           |
| **DICE**             | Bulk RNA-seq                 | 12 flow-sorted immune cell types     |
| **PRIDE (OTAR3091)** | Mass spectrometry proteomics | 74 tissues                           |

***

## Data Sources

### Tabula Sapiens

[Tabula Sapiens v2](https://tabula-sapiens-portal.ds.czbiohub.org/) is a single-cell transcriptomic atlas containing over 1.1 million cells spanning multiple human organs and tissues. The atlas was generated from samples collected from 24 human donors using single-cell RNA sequencing technologies and annotated into cell types by domain experts.

### Genotype-Tissue Expression (GTEx) Program

The [Genotype-Tissue Expression (GTEx) Program](https://gtexportal.org/home/) aims to build a comprehensive public resource for studying tissue-specific gene expression and its relationship to genetic variation. The GTEx v10 dataset contains bulk RNA-seq data from 54 tissues collected from 946 human donors.

### Database of Immune Cells (DICE)

The [Database of Immune Cells (DICE)](https://dice-database.org/) provides gene expression profiles from 12 flow-sorted immune cell types derived from peripheral blood samples from 91 healthy donors. Open Targets uses DICE build 2.23.2022. The data were generated using bulk RNA sequencing.

### PRIDE (Proteomics Identifications Database)&#x20;

[PRIDE](https://www.ebi.ac.uk/pride/archive/) is a public repository for proteomics data. As part of an Open Targets project, the PRIDE team reanalysed four human proteomics datasets to provide protein expression measurements across multiple human tissues.

The following datasets were included:

| **Dataset**                                                         | **Description**           |
| ------------------------------------------------------------------- | ------------------------- |
| [PXD000561](https://www.ebi.ac.uk/pride/archive/projects/PXD000561) | 21 tissues from 6 donors  |
| [PXD000865](https://www.ebi.ac.uk/pride/archive/projects/PXD000865) | 34 tissues from 1 donor   |
| [PXD020192](https://www.ebi.ac.uk/pride/archive/projects/PXD020192) | 46 tissues from 2 donors  |
| [PXD016999](https://www.ebi.ac.uk/pride/archive/projects/PXD016999) | 32 tissues from 14 donors |

## Computational pipelines and datasets

#### Initial data processing

**Single-cell RNA-sequencing (scRNA-seq) data from Tabula Sapiens**

Single-cell RNA-sequencing data for tissues and cell types was downloaded from the [Tabula Sapiens portal](https://tabula-sapiens-portal.ds.czbiohub.org/) as AnnData files containing raw count matrices with the associated metadata. The data were then processed into pseudobulked expression profiles for each cell type, each tissue, and each cell type within each tissue. The pseudobulked expression profiles are generated with a dSum approach as described in [Cuomo et al. 2021](https://doi.org/10.1186/s13059-021-02407-x). In short, in order to obtain a pseudobulked sample we sum the raw counts of each gene across all cells within a donor for a given annotation (tissue, cell type or cell type within tissue). This results in one pseudobulked expression sample per donor per annotation. The summed counts are then normalised using the CPM (Counts Per Million) approach.

The result is three pseudobulked expression datasets: cell type, tissue, and cell type within tissue.

**Bulk RNA-sequencing (RNA-seq) data from GTEx and DICE**

Bulk RNA-sequencing data for tissues was downloaded in transcripts per million (TPM) units from the [GTEx portal](https://gtexportal.org/home/downloads/adult-gtex/bulk_tissue_expression) and for cell types from the [DICE portal](https://dice-database.org/downloads).

**Mass spectrometry (MS)-based proteomics data from PRIDE**

Baseline mass spectrometry–based proteomics data were compiled from selected public PRIDE datasets curated using SDRF proteomics metadata guidelines. Raw files in these datasets had been reanalysed centrally using the open-source tools MaxQuant (version 2.7.0.0) according to predefined dataset selection and curation guidelines, and the resulting protein-level quantification tables with associated SDRF metadata were downloaded from the [PRIDE FTP ](https://www.ebi.ac.uk/pride/archive/)resource.

#### Generating unaggregated expression profiles

All baseline expression data are processed into a unified set of unaggregated, donor-level expression profiles. We harmonise metadata and map tissue and cell type annotations to standardised ontologies: [UBERON](https://www.ebi.ac.uk/ols4/ontologies/uberon) and the [Cell Ontology](https://www.ebi.ac.uk/ols4/ontologies/cl). If a donor has multiple samples for the same annotation, we calculate the mean expression to produce a single value for each donor-annotation pair. The data structure is standardised, but expression values retain their original units: TPM for bulk RNA-seq, pseudobulk CPM (sum\[counts]) for pseudobulked scRNA-seq, and PPB (iBAQ) for proteomics.

#### Generating aggregated expression profiles

We aggregate the donor-level data to produce a summary of expression for each target in each tissue or cell type. This includes:

* **Expression Quartiles**: We calculate the minimum, 25th percentile, median, 75th percentile, and maximum expression values across all donors for a given annotation.
* **Expression Distribution Score**: We compute a score representing the breadth of expression within a dataset, defined as the proportion of annotations in which the target is expressed above a threshold of 0.5 (unit) median expression. The threshold is chosen to minimise the impact of noise (e.g. from ambient RNA).
* **Expression Specificity Score**: We use the tool CELLEX ([Timshel et al. 2020](https://doi.org/10.7554/eLife.55851)) which combines four expression-specificity metrics into a single, ranked specificity score that reflects how specifically a gene is expressed in a given annotation relative to all other annotations in that dataset. Because ranking is done within each annotation, a gene expressed in a tissue expressing many genes must have stronger specificity to rank highly than it would in a tissue with fewer distinct markers. Consequently, the annotation with the highest expression is not always the one where the gene has the highest specificity score. For a given gene, specificity is denoted as “high” for annotations where the gene is scored amongst the top 25% of specifically expressed genes.

To enable comparisons across similar tissues and cell types from different data sources, we also assign a set of high-level, parental tissue and cell type categories to each annotation. The parental labels are derived from manual grouping of the ontology mappings, for example, the heart left ventricle from GTEx and cardiac atrium from Tabula Sapiens both share the parental label of heart. There are 37 parental tissue labels and 24 parental cell type labels.

## Data Availability

These datasets can be accessed via the [Platform web interface](https://platform.opentargets.org/target/ENSG00000133703)**,** [download page](https://platform.opentargets.org/downloads) and GraphQL [API](https://platform.opentargets.org/api).

<figure><img src="../.gitbook/assets/Screenshot 2026-06-23 at 14.35.24.png" alt=""><figcaption></figcaption></figure>

<sub>Example of new baseline expression widget for</sub> <sub></sub><sub>**KRAS**</sub><sub>.</sub>

## Publications

* GTEx Consortium. _**The GTEx Consortium atlas of genetic regulatory effects across human tissues**_**.** Science. 2020;369(6509):1318–1330.
* The Tabula Sapiens Consortium. _**The Tabula Sapiens: A multiple-organ, single-cell transcriptomic atlas of humans**_**.** Science. 2022;376(6594).
* Ha B, et al. _**Database of Immune Cell eQTLs, Expression, Epigenomics**_**.** The Journal of Immunology. 2019;202(1 Supplement):131.18.
* Perez-Riverol Y, et al. _**The PRIDE database at 20 years: 2025 update**_**.** Nucleic Acids Research. 2025;53(D1)–D553.
* Tyanova S, et al. _**The MaxQuant computational platform for mass spectrometry-based shotgun proteomics**_**.** Nature Protocols. 2016;11(12):2301–2319.
* Cuomo AS, et al. _**Optimizing expression quantitative trait locus mapping workflows for single-cell studies**_**.** Genome Biology. 2021;22(1):240.
* Timshel P, et al. _**Genetic mapping of etiologic brain cell types for obesity**_**.** eLife. 2020;9.
