# Baseline expression

## Overview

Baseline RNA and protein expression data helps us to ascertain whether the target is expressed in all tissues or selectively in one or few tissues or cell types. The availability of the target molecule in the location of interest is critical at different stages of the drug development process.

We combine baseline expression information from three sources:

* **Expression Atlas**: RNA expression meta-analysis from RNA- sequencing experiments
* **Human Protein Atlas**: immunohistochemistry-based proteomics data for normal tissues
* **Genotype-Tissue Expression (GTEx) Program**: RNA baseline expression variation data per tissue

## Data sources

### Expression Atlas

Expression Atlas - [https://www.ebi.ac.uk/gxa/home](https://www.ebi.ac.uk/gxa/home) - is a manually-curated, freely available data analysis and visualisation resource that provides information about gene and protein expression in more than 3,000 experiments.

### Human Protein Atlas

The Human Protein Atlas - [https://www.proteinatlas.org](https://www.proteinatlas.org) - is an international collaboration that develops various open access knowledge resources that map all the human proteins in cells, tissues and organs using an integration of various 'omics technologies. The Human Protein Atlas consists of six separate parts, each focusing on a particular aspect of the genome-wide analysis of the human proteins. At the moment, we only use the [Tissue Atlas](https://www.proteinatlas.org/humanproteome/tissue), showing the distribution of the proteins across all major tissues and organs in the human body.

### Genotype-Tissue Expression (GTEx) Portal

The Genotype-Tissue Expression (GTEx) Portal - [https://gtexportal.org/home/](https://gtexportal.org/home/) - is an open access data resource that provides data on gene expression, QTLs, and histology images. The Portal is part of the GTEx consortium's ongoing effort to build a comprehensive public resource to study tissue-specific gene expression and regulation and its relationship to genetic variation.

## Computational pipelines and datasets

#### RNA expression meta-analysis

Open Targets in collaboration with Expression Atlas has performed a meta-analysis of over 18,000 samples from 50 different tissues and more than 30 cell types from the following experiments:

* RNA-seq of 53 human tissue samples from GTEx ([E-MTAB-5214](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-5214/Results))
* RNA-seq of 16 human tissues from the Illumina Body Map project ([E-MTAB-513](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-513/Results))
* RNA-seq of 13 human tissue from the ENCODE project (Snyder Lab) ([E-MTAB-4344](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-4344/Results))
* RNA-seq of 6 human tissues from Kaessmann Lab ([E-MTAB-3716](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-3716/Results))
* mRNA-seq of 32 human tissues from Human Protein Atlas ([E-MTAB-2836](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-2836/Results))
* mRNA-seq of rare types of cells of different haemopoietic lineages from healthy individuals in the BLUEPRINT project ([E-MTAB-3819](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-3819/Results))
* RNA-seq of common types of cells of different haemopoietic lineages from healthy individuals in the BLUEPRINT project ([E-MTAB-3827](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-3827/Results))
* mRNA-seq of plasma cells of tonsil from healthy individuals from the BLUEPRINT project ([E-MTAB-4754](https://www.ebi.ac.uk/gxa/experiments/E-MTAB-4754/Results))

The tissue- and cell-based samples in these experiments are processed separately to avoid batch effects during normalisation. The samples of each group are then processed together to generate an expression table of normalised Transcripts Per Million (TPMs) units for every gene in each tissue or cell type according to the following steps:

* Technical replicates are aggregated
* Genes that are expressed below a pre-defined threshold (i.e. minimum of 10 raw reads in at least 15 samples) are filtered out
* Samples are then normalised in a two-step process according to [Risso et al. 2014](https://europepmc.org/article/MED/25150836) using the RUV (Remove Unwanted Variation) method:
  * The Coefficient of Variation (CV) was estimated for each gene across all the samples and used to select the least variable genes.
  * The least variable 1,000 genes were used as negative controls; that is, assumed not to be differentially expressed, to train RUVg to remove unwanted variation
* Tissues are mapped to anatomical ontology terms using the [Uber-anatomy ontology](https://www.ebi.ac.uk/ols/ontologies/uberon). Tissues that can't be mapped are then discarded
* Samples from the same tissue across different experiments are averaged by median and then merged in the final matrix
* Expression tables of the tissue- and cell-based experiments are combined

We analyse this expression file further to compute two values for each gene:

* **Binned value of expression:** The normalised expression values are divided into 10 bins of the same width. Note that this is not the same as the deciles, which all contain the same number of items in them
* **Tissue specificity**: Z-scores are calculated for each gene and each tissue and then they are binned based on quantiles of a perfect normal distribution. We compute the tissue specificity of a target as the number of standard deviations from the mean of the log RNA expression of the target across the available tissues. A target is considered to be tissue specific if the z-score is greater than 0.674 (or the 75th percentile of a perfect normal distribution). We remove data for under-expressed targets before the z-score calculation. This allows us to extract the tissues for which a gene is specific, defined as the expression value being above the 75th z-score percentile - in practice, anything in bin 2 or above.

Normalised files with binned value of expression and tissue specificity values for each target are available from [our data download page](https://platform.opentargets.org/downloads).

## Publications

GTEx Consortium. **The Genotype-Tissue Expression (GTEx) project**. Nat Genet. 2013 Jun;45(6):580-5. doi: [10.1038/ng.2653](https://doi.org/10.1038/ng.2653). PMID: [23715323](https://pubmed.ncbi.nlm.nih.gov/23715323/); PMCID: PMC4010069.

Papatheodorou I, Moreno P, Manning J, Fuentes AM, George N, Fexova S, Fonseca NA, Füllgrabe A, Green M, Huang N, Huerta L, Iqbal H, Jianu M, Mohammed S, Zhao L, Jarnuczak AF, Jupp S, Marioni J, Meyer K, Petryszak R, Prada Medina CA, Talavera-López C, Teichmann S, Vizcaino JA, Brazma A. **Expression Atlas update: from tissues to single cells**. Nucleic Acids Res. 2020 Jan 8;48(D1):D77-D83. doi: 10.1093/nar/gkz947. PMID: [31665515](https://pubmed.ncbi.nlm.nih.gov/31665515/); PMCID: PMC7145605.

Uhlén M, Fagerberg L, Hallström BM, Lindskog C, Oksvold P, Mardinoglu A, Sivertsson Å, Kampf C, Sjöstedt E, Asplund A, Olsson I, Edlund K, Lundberg E, Navani S, Szigyarto CA, Odeberg J, Djureinovic D, Takanen JO, Hober S, Alm T, Edqvist PH, Berling H, Tegel H, Mulder J, Rockberg J, Nilsson P, Schwenk JM, Hamsten M, von Feilitzen K, Forsberg M, Persson L, Johansson F, Zwahlen M, von Heijne G, Nielsen J, Pontén F. Proteomics. **Tissue-based map of the human proteome**. Science. 2015 Jan 23;347(6220):1260419. doi: 10.1126/science.1260419. PMID: [25613900](https://pubmed.ncbi.nlm.nih.gov/25613900/).
