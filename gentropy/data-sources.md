---
description: Overview of the GWAS association and functional genomics data sources
---

# Data sources

The Platform ingests GWAS, functional genomics and additional datasets to aid the interpretation of the observed signals. These include:

## NHGRI-EBI GWAS Catalog

🌍 [Website](https://www.ebi.ac.uk/gwas/) — 📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/gwas_catalog/_gwas_catalog/)

The [NHGRI-EBI GWAS Catalog](https://www.ebi.ac.uk/gwas/) is a data source that provides detailed, structured genome-wide association study data in standardised format of summary statistics and curated associations (top-hits) to [EFO](https://www.ebi.ac.uk/efo/) traits. We rely on the GWAS Catalog for a rich source of genetic associations, utilising the data for analysis and interpretation.

The GWAS Catalog information feeds the Open Targets Platform by providing study metadata and GWAS associations from two sources:&#x20;

### **GWAS Catalog literature-curated associations (GCCA)**

The Platform ingests the GWAS Catalog curated associations (top-hits) from the table “All associations - with added ontology annotations, GWAS Catalog study accession numbers and genotyping technology” (see [GWAS Catalog download page](https://www.ebi.ac.uk/gwas/docs/file-downloads)).  The GWAS Catalog curation process may result in multiple GWAS being grouped under one study accession, in which case one study accession will need to be split into multiple studies in the Platform. An example of such a study is: [GCST001762](https://www.ebi.ac.uk/gwas/studies/GCST001762), where the reported trait is 'Obesity-related traits', but the underlying association data informs which top-hit comes from which specific trait, for example 'BMI z-score change'. In this case, we create as many new studies as there are association-level trait annotations. The new study identifiers are generated from the original study accession plus a suffix. The disease annotations of the newly created studies are inherited from the association data. A similar action is required when results from different ancestries are pooled under one study accession.&#x20;

The harmonisation process includes a number of steps that flag any associations with quality concerns. When harmonising GCCA, the following cases were flagged:

* Variant interaction associations
* Variant location is not available in an association source
* Variant location data is inconsistent (chromosome and position values don’t match)
* Lead variant is duplicated for the same study
* The provided variant location doesn’t match any GnomAD variant
* The risk allele couldn't be mapped to the GnomAD reference
* The lead variant had palindromic alleles
* The lead variant p-value was above the genome-wide significant threshold (p-value>1e-8).

Curated associations were converted into the Gentropy `StudyLocus` format and uniformly flagged with `Study locus from curated top hit` quality control flag. Corresponding `StudyIndex` are generated to captures the study metadata.

### **GWAS Catalog Summary Statistics  (GCSS)**

The Platform ingests GWAS Catalog studies from full summary statistics when they have been harmonised following the [protocol](https://www.ebi.ac.uk/gwas/docs/methods/summary-statistics). Each harmonised study is converted into a Gentropy `SummaryStatistics` format as described in the [Gentropy documentation](https://opentargets.github.io/gentropy/python_api/datasets/summary_statistics/) including additional quality controls:

1. filtering out SNPs with unavailable beta, standard error, or p-value
2. filtering out SNPs with zero or Inf values for beta and standard error
3. filtering out SNPs with negative p-values or standard error
4. filtering out SNPs with p-values equal to 1

In some cases, this results in empty `SummaryStatistics`datasets and these studies are excluded from further analysis.&#x20;

#### **GCSS studies manual curation**

The Open Targets team performs additional manual curation for the GCSS studies from “All studies - With study accession numbers, ontology annotations, genotyping technology, cohort identifiers and full summary statistics availability”. The following information is extracted from the corresponding publication:

1. **Study type** — The GCSS studies identified as pQTL or microbiome GWAS are flagged and excluded from further analysis.
2. **Analysis type** — studies are flag if performed with any of the following analysis: multivariate analysis, ExWAS, non-additive model, metabolite, GxG, GxE, case-case study. All analysis flags but “metabolite” are excluded from SuSiE fine-mapping and fine-mapped using PICS.

A `StudyIndex`dataset was created as part of this pipeline containing all the available metadata for the included GWAS Catalog studies. If available, the ancestries from GWAS Catalog were mapped to gnomAD ancestry suffixes using [the dictionary here](https://github.com/opentargets/gentropy/blob/dev/src/gentropy/assets/data/gwas_population_2_LD_panel_map.json). The ancestry wasn't assigned if the ancestry was unavailable or wasn't presented in the dictionary.

#### **GCSS** quality control

GWAS summary statistics quality control (QC) is performed for all GWAS Catalog studies with available summary statistics, following the methods described in [Winkler et al. (2014)](https://www.nature.com/articles/nprot.2014.071):

1. **The P-Z test**. This check estimates the mean and standard deviation of the difference between the log p-values reported in the study and the reported betas and standard errors. If at least one value for the study was greater than 0.05, the study fails QC and is flagged with the label `The PZ QC check values are not within the expected range`.
2. **The mean beta check**. This check estimates the mean value of the beta across all SNPs in the study. If the absolute mean value is more than 0.05, the study fails QC and is flagged with the label `The mean beta QC check value is not within the expected range`.
3. **The genomic control (GC) lambda check**. This check estimates the additive GC lambda of the study (see [Tsepilov et al. (2013)](https://pubmed.ncbi.nlm.nih.gov/24358113/)). If the GC lambda value is outside the \[0.7,2.5] range the study fails QC and is flagged with the label `The GC lambda value is not within the expected range`.
4. **Number of variants.** All summary statistics with fewer than 2,000,000 variants do not fail QC but are flagged with the label `The number of SNPs in the study is below the expected threshold`. These studies are not eligible for SuSiE fine-mapping.

## FinnGen

🌍 [Website](https://www.finngen.fi/en) — 📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/finngen/_finngen/)

[FinnGen](https://www.finngen.fi/en) is an academia-industry partnership that aims to produce genome variant data for 500,000 Finns. The genomic data is then combined with phenotype data collected by national health registries, including extensive longitudinal registry data available on all Finns. More details on the protocols are available [in the FinnGen documentation](https://finngen.gitbook.io/documentation/releases). Because the Finnish population has been genetically isolated, fine-mapping was performed with a suitable reference panel of LD. The Platform includes the fine-mapping results from the FinnGen team using SuSiE and FINEMAP, based on a reference panel of whole genome sequencing data from Finns.

The Platform includes the 95% credible sets as [described in the documentation](https://finngen.gitbook.io/documentation/data-description) after converting them Gentropy `StudyIndex` and `StudyLocus` objects. Credible sets with a lead SNP p-value>=1e-5 are marked with a `Subsignificant p-value` flag.

## eQTL Catalogue

🌍 [Website](https://www.ebi.ac.uk/eqtl/) — 📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/eqtl_catalogue/_eqtl_catalogue/)

The [eQTL Catalogue](https://www.ebi.ac.uk/eqtl/) aims to provide unified gene expression, protein-level and splicing QTLs from publicly available human public studies. Using a standardised pipeline ([QTLmap](https://github.com/eQTL-Catalogue/qtlmap)), the eQTL catalogue is integrated in the Platform as a rich source of molecular QTLs (molQTLs). The pipeline uses SuSiE as the method of fine-mapping and results in 95% CSs.

All credible sets and study information are reformatted to Gentropy's `StudyIndex` and `StudyLocus` datasets. Credible sets with a lead SNP p-value>=1e-3 are marked with a `Subsignificant p-value` flag.&#x20;

## The Pharma Proteomics UK Biobank Project (PPP-UKBB)&#x20;

&#x20;📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/ukb_ppp_eur/_ukb_ppp_eur/)

[The Pharma Proteomics Project](https://www.synapse.org/Synapse:syn51364943/wiki/622119) is a pre-competitive biopharmaceutical consortium characterising the plasma proteomic profiles of 54,219 participants in the UK Biobank.&#x20;

The Platform includes GWAS full summary statistics for 2,954 proteins of European ancestry [from the Synapse platform](https://www.synapse.org/Synapse:syn51364943/wiki/622119). Data is converted to `SummaryStatistics` and `StudyIndex` format applying the following modifications:

* SNPs with MAF<1e-4 and INFO<0.8 are filtered out
* Align the order of effective and reference alleles with the gnomAD annotation: if the alleles are reversed, the sign of the effect size is changed; if the allele combination do not match the reference, the SNP is filtered out
* Flag QTLs as _cis_ or _trans_ based on a 5Mb window from the affected gene.

## gnomAD

🌍[Website](https://gnomad.broadinstitute.org/) — 📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/gnomad/_gnomad/)

[gnomAD](https://gnomad.broadinstitute.org/) (Genome Aggregation Database) is a comprehensive resource that provides aggregated genomic data from large-scale sequencing projects. It encompasses variants from diverse populations and is widely used for variant annotation and population genetics studies.

### Variant annotation

GnomAD (v4) variant annotation is used to provide extra annotation for variants included in the Platform and assist some of our harmonisation pipelines. Among the most relevant annotations included are: population allelic frequencies, in silico predictors and cross-references. All variants are available in GRCh38 coordinates.

### LD matrices

gnomAD v2.1.1 [LD matrices](https://gnomad.broadinstitute.org/news/2018-10-gnomad-v2-1/) are used to create a multi-ancestry LD reference for the [PICS fine-mapping method](fine-mapping.md#pics-fine-mapping). All variants are liftovered to build GRCh38.

## Pan-UKBB LD matrices

🌍 [Website](https://pan.ukbb.broadinstitute.org/docs/summary/index.html)

The Platform uses [Pan-UK Biobank project](https://pan.ukbb.broadinstitute.org/docs/summary) LD matrices for three ancestries: Non-Finnish European (NFE), Central/South Asian (CSA) and African (AFR). See the descriptive summary [from Pan-UK Biobank](https://pan.ukbb.broadinstitute.org/docs/technical-overview). The LD was computed for each chromosome in 10 Mb radius. Only SNPs with INFO > 0.8, MAC > 20 in each population are used to calculate LD. Matrices are stored in hail BlockMatrix format. We use these LD matrices for SuSiE fine-mapping.

## EMBL-EBI Ensembl

🌍 [Website](https://www.ensembl.org/index.html) — 📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/ensembl/_ensembl/)

The Platform uses Ensembl as a source of gene, transcript and variant annotations. Affected genes in QTL studies are validated using fixed version of Ensembl and all variants are annotated using Ensembl VEP.

## Biosample

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasources/biosample_ontologies/_cell_ontology/)

The Experimental Factor Ontology, UBERON and Cell Ontology are composed as a meta-ontology to capture every tissue or cell type that could be described in a QTL study.



