# 🆕 Study

## Overview

In the Open Targets Platform, a study is a qualifying genome-wide association study for binary or quantitative traits.

Studies might capture different types of associations, such as curated associations (top hits) from literature or post-processing GWAS summary statistics.

For each study meeting the [inclusion criteria](study.md#study-inclusion-criteria), harmonisation, [fine-mapping](gentropy/fine-mapping.md), [colocalisation](gentropy/colocalisation.md), and [Locus-to-Gene](gentropy/locus-to-gene-l2g.md) analysis are performed, resulting in a list of significant credible sets and their most likely associated genes. The resulting 95% credible sets can be visualised in all study pages. Within the same study, credible sets might result from different fine-mapping pipelines but still be presented in the same study with their respective provenance and confidence.&#x20;

{% hint style="info" %}
**Studies without GWAS-significant associations**

The study will still be presented in the Open Targets Platform if no significant associations are found.&#x20;
{% endhint %}

#### **Key study annotation**

To provide a rich context to downstream interpretation of studies, and their associations, we capture a wide range annotations, whenever possible in a standardised way to enable interoperability.&#x20;

For example:

* The measured trait/phenotype is standardised using the Experimental Factor Ontology ([EFO](https://www.ebi.ac.uk/efo/)), as the background trait when applied
* For molecular QTLs, the affected gene/protein is standardised to Ensembl gene identifiers
* For molecular QTLs, the biological context is standardised to relevant ontology (e.g. tissue — [UBERON](https://www.ebi.ac.uk/ols4/ontologies/uberon) or cell ontology — [CL](https://www.ebi.ac.uk/ols4/ontologies/cl))
* Depending on the granularity of the ingested study metadata, a rich cohort information is captured including sample sizes, ancestry composition and a list of named cohorts
* Indicated if association data of a study was ingested as summary statistics, together with the corresponding quality control measurements performed on the summary statistics
* Besides the Pubmed identifier, rich publication information is also captured including first author, publication year for easier data access

## Study categories

Integrated studies can be split into two major groups that determine how their associations would be utilised in the target identification process.&#x20;

### 1. Genome-wide association studies (GWAS)

A GWAS identifies associations between genetic variants and traits or phenotypes by analysing genome-wide variation data from a population. These studies cover binary or quantitative traits reported in the integrated sources.

{% hint style="info" %}
**Shared trait studies**&#x20;

GWAS studies sharing the same disease or phenotype (EFO) as the study are listed.
{% endhint %}

**Sources**: [GWAS Catalog](https://www.ebi.ac.uk/gwas/), [FinnGen](https://www.finngen.fi/en/access_results)

### 2. molQTL studies

A molQTL study identifies genetic variation that can be significantly associated with changes at the molecular level. As such, associations of these studies provide invaluable help to put GWAS derived loci into context via [colocalisation](gentropy/colocalisation.md). The type of molecular trait measured defines the type of QTL:&#x20;

* eQTLs impact gene expression
* pQTLs impact protein abundance
* sQTLs have an effect on gene splicing
* tuQTLs impact transcript usage
* sceQTL impact gene expression at the single-cell level

{% hint style="info" %}
All molQTL studies are annotated with the gene whose expression levels are regulated, referred as the affected gene.

On top of the effected gene, molQTL studies also capture the tissue/cell type in which the change in the molecular trait was measure providing further context for interpretation.
{% endhint %}

Each molQTL study captures the unique combination of the following annotations:

* The publication authoring the study
* The gene product measured in the study&#x20;
* The quantitative method (e.g. aptamer) used to measure the trait, when available
* The cell type or tissue where the trait is measured, when available
* The experimental conditions (e.g. interferon-stimulated macrophages)

**Sources**: [eQTL Catalogue](https://www.ebi.ac.uk/eqtl/), [UK Biobank Pharma Proteomics Project](https://www.synapse.org/Synapse:syn51364943/wiki/622119) (UKB-PPP)

## Study inclusion criteria

Studies must meet predefined criteria to ensure consistent representation, and increased reliability of associations for downstream analysis.&#x20;

**Each integrated study needs to meet the following criteria**:

* GWAS studies need to have a valid disease or phenotype identifier (EFO)
* QTL studies must have an affected gene and tissue/cell-type valid identifier (biosample)
* Valid study type (e.g `gwas` or a QTL type from a defined set)
* Data licensed for commercial usage
* When summary statistics are available, further [criteria](gentropy/data-sources.md#gcss-quality-control) must be met:
  * Mean beta within expected range
  * Genomic control (GC) lambda value within the expected range
  * The PZ value within the expected range
  * Additional [curation](gentropy/data-sources.md#gcss-studies-manual-curation) from Open Targets team ensuring study meet standards

## GWAS/molQTL credible sets

The [fine-mapping](gentropy/fine-mapping.md) results for all 95% credible sets in the study are displayed with their most relevant metadata, as well as the top [Locus-to-Gene](gentropy/locus-to-gene-l2g.md) assignment.

Because the same study might be processed through different fine-mapping pipelines, it's possible to observe credible sets obtained with different methods even within the same study. The [credible set exclusion criteria](credible-set.md#credible-set-exclusion-criteria) describes the rules applied to avoid duplicated credible sets resulting from separate fine-mapping pipelines.

Source: [Open Targets](gentropy/fine-mapping.md)
