---
description: Overview of the Open Targets Locus-to-Gene algorithm
---

# Locus-to-Gene (L2G)

Based on genetic and functional genomics traits, the Locus-to-Gene (L2G) machine-learning algorithm ranks the most likely causative genes at each GWAS credible set. The likelihood that a gene is causal for a particular GWAS locus is measured by the L2G score, ranging from 0 to 1.

{% hint style="warning" %}
The L2G model included in the Platform is based on the original method published by Mountjoy _et al._ Nature Genetics (2021), but contains several enhancements that can result in different performance.
{% endhint %}

## Features

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasets/l2g_features/_l2g_feature/)

The predictive features used by the L2G algorithm are designed to capture various genetic and genomic contexts that influence the likelihood of a gene being causal at a given GWAS credible set.&#x20;

Features are divided into four categories:&#x20;

{% tabs %}
{% tab title="Distance" %}


<table><thead><tr><th width="362.13671875">Feature Name</th><th width="355.55859375">Description</th><th width="183.2421875">Range</th></tr></thead><tbody><tr><td><code>distanceTssMean</code></td><td>Average distance between all variants in the credible set and the TSS of a gene's canonical transcript. The distance of each variant is weighted by its posterior probability</td><td>(0, 1)</td></tr><tr><td><code>distanceTssMeanNeighbourhood</code></td><td>Ratio between <code>distanceTssMean</code> for a gene and the maximum <code>distanceTssMean</code> for any given gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>distanceSentinelTss</code></td><td>Distance between the sentinel variant and the TSS of a gene's canonical transcript</td><td>(0, 1)</td></tr><tr><td><code>distanceSentinelTssNeighbourhood</code></td><td>Ratio between <code>distanceSentinelTss</code> for a gene and the maximum <code>distanceSentinelTss</code> for any given gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>distanceSentinelFootprint</code></td><td>Distance between sentinel variant and a gene's footprint</td><td>(0, 1)</td></tr><tr><td><code>distanceSentinelFootprintNeighbourhood</code></td><td>Ratio between <code>distanceSentinelFootprint</code> for a gene and the maximum <code>distanceSentinelFootprint</code> for any given gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>distanceFootprintMean</code></td><td>Average distance between all variants in the credible set and a gene's footprint. The distance of each variant is weighted by its posterior probability</td><td>(0, 1)</td></tr><tr><td><code>distanceFootprintMeanNeighbourhood</code></td><td>Ratio between <code>distanceFootprintMean</code> for a gene and the maximum <code>distanceFootprintMean</code> for any given gene in the vicinity</td><td>(0, 1)</td></tr></tbody></table>
{% endtab %}

{% tab title="Colocalisation" %}


<table><thead><tr><th width="335.04296875">Feature Name</th><th width="287.00390625">Description</th><th>Range</th></tr></thead><tbody><tr><td><code>eQtlColocClppMaximum</code></td><td>Maximum CCLP across all eQTL studies for a gene</td><td>(0, 1)</td></tr><tr><td><code>pQtlColocClppMaximum</code></td><td>Maximum CCLP across all pQTL studies for a gene</td><td>(0, 1)</td></tr><tr><td><code>sQtlColocClppMaximum</code></td><td>Maximum CCLP across all sQTL and tuQTL studies for a gene</td><td>(0, 1)</td></tr><tr><td><code>eQtlColocH4Maximum</code></td><td>Maximum H4 across all eQTL studies for a gene</td><td>(0, 1)</td></tr><tr><td><code>pQtlColocH4Maximum</code></td><td>Maximum H4 across all pQTL studies for a gene</td><td>(0, 1)</td></tr><tr><td><code>sQtlColocH4Maximum</code></td><td>Maximum H4 across all sQTL and tuQTL studies for a gene</td><td>(0, 1)</td></tr><tr><td><code>eQtlColocClppMaximumNeighbourhood</code></td><td>Ratio between <code>eQtlColocClppMaximum</code> for a gene and the maximum <code>eQtlColocClppMaximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>pQtlColocClppMaximumNeighbourhood</code></td><td>Ratio between <code>pQtlColocClppMaximum</code> for a gene and the maximum <code>pQtlColocClppMaximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>sQtlColocClppMaximumNeighbourhood</code></td><td>Ratio between <code>sQtlColocClppMaximum</code> for a gene and the maximum <code>sQtlColocClppMaximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>eQtlColocH4MaximumNeighbourhood</code></td><td>Ratio between <code>eQtlColocH4Maximum</code> for a gene and the maximum <code>eQtlColocH4Maximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>pQtlColocH4MaximumNeighbourhood</code></td><td>Ratio between <code>pQtlColocH4Maximum</code> for a gene and the maximum <code>pQtlColocH4Maximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>sQtlColocH4MaximumNeighbourhood</code></td><td>Ratio between <code>sQtlColocH4Maximum</code> for a gene and the maximum <code>sQtlColocH4Maximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr></tbody></table>


{% endtab %}

{% tab title="Variant Effect" %}


<table><thead><tr><th width="233.84765625">Feature Name</th><th width="384.11328125">Description</th><th>Range</th></tr></thead><tbody><tr><td><code>vepMaximum</code></td><td>Maximum VEP score across all variants in the credible set</td><td>(0, 1)</td></tr><tr><td><code>vepMaximumNeighbourhood</code></td><td>Ratio between <code>vepMaximum</code> for a gene and the maximum <code>vepMaximum</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr><tr><td><code>vepMean</code></td><td>Average VEP score between all variants in the credible set and a gene's footprint. The score of each variant is weighted by its posterior probability</td><td>(0, 1)</td></tr><tr><td><code>vepMeanNeighbourhood</code></td><td>Ratio between <code>vepMean</code> for a gene and the maximum <code>vepMean</code> for any protein-coding gene in the vicinity</td><td>(0, 1)</td></tr></tbody></table>


{% endtab %}

{% tab title="Other" %}
<table><thead><tr><th>Feature Name</th><th width="491.48046875">Description</th><th>Range</th></tr></thead><tbody><tr><td><code>geneCount500kb</code></td><td>Number of genes 250kb up- and down-stream the sentinel variant of a credible set</td><td>(0, 60000)</td></tr><tr><td><code>proteinGeneCount500kb</code></td><td>Number of protein-coding genes 250kb up- and down-stream the sentinel variant of a credible set</td><td>(0, 60000)</td></tr><tr><td><code>credibleSetConfidence</code></td><td>Degree of confidence we assign to the credible set definition based on the fine mapping methodology: 1 when fine-mapped with SuSIE using in-sample LD: 0.75 when fine-mapped with SuSIE using out-of-sample LD: 0.5, when fine-mapped with PICS and the locus is based on the analysis of summary statistics; 0.25, when fine-mapped with PICS and the locus was reported as a top hit according to the GWAS Catalog</td><td>(0, 1)</td></tr></tbody></table>


{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Neighbourhood features**

While some features are computed independently for each gene, others reflect the comparative relative context of a given gene compared to the other genes in the neighbourhood (+/- 500,000bp).&#x20;
{% endhint %}

{% hint style="info" %}
For a more detailed description of how each feature is computed, see [the L2G Feature documentation](https://opentargets.github.io/gentropy/python_api/datasets/l2g_features/_l2g_feature/).
{% endhint %}

## Training set

The L2G model is trained based on prior knowledge of gene-trait associations collated from different sources, to later bring representative credible sets supporting that association. The next steps describe the methodology to compose the training set:

#### **Effector gene list**

The **effector gene list (EGL)** represents the set of biologically validated gene-trait associations. This list is derived from several sources:

1. Manually curated [gold standards](https://github.com/opentargets/genetics-gold-standards) (“medium” and “high” confidence) from OTG 22.10.
2. Gene-indication pairs for the pharmacological target in all phase III or IV clinical trials according to the latest ChEMBL release.
3. Gene-disease or phenotype mappings with evidence score ≥ 0.95 from [ClinVar](https://platform-docs.opentargets.org/evidence#clinvar), [UniProt](https://platform-docs.opentargets.org/evidence#uniprot-variants), [Gene2Phenotype](https://platform-docs.opentargets.org/evidence#gene2phenotype), [Genomics England PanelApp](https://platform-docs.opentargets.org/evidence#genomics-england-panelapp) and [ClinGen](https://platform-docs.opentargets.org/evidence#clingen) from the latest Open Targets Platform release.

To ensure the uniqueness of gene-EFO pairs, the combined list was de-duplicated.

#### **Positives**

For each gene-trait pair from the effector gene list, positive gene-credible set pairs were extracted using the following criteria:

1. Only protein-coding genes.
2. Removed any pair with a `distanceSentinelTSS` feature less than 0.1.
3. Only include gene-trait pairs supported by at least two credible sets in different studies sharing the same lead variant. We added this criterion to reduce the chance of false positives among the credible sets.
4. Among all positive credible set-gene pairs, we removed duplications based on functional genomics features.
5. Removed credible sets involved in more than two positives.

#### **Negatives**

All other protein-coding genes in the window are classified as negatives as long as they don't have a strong functional interaction (STRINGdb score > 0.8) with any positive genes for the trait.

## The L2G model

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/l2g/model/)

The Locus-to-Gene model is trained for every data release using the training set and feature matrix following. Similarly to Mountjoy _et al._, the model is trained based on a gradient-boosting algorithm with the `scikit-learn` library, and using nested cross-validation and hyperparameter tuning.

{% embed url="https://huggingface.co/opentargets/locus_to_gene" %}
The L2G model is available on Hugging Face and in the FTP location&#x20;
{% endembed %}

{% hint style="info" %}
The L2G model will be updated in each release to include new features and/or fixes. You should expect some variation in the prediction scores with each release.
{% endhint %}

## L2G predictions

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/datasets/l2g_prediction/)

The trained L2G model is applied to every GWAS credible set in the Open Targets Platform. All predictions below 0.05 are filtered out and feature contributions are added using SHAP analysis as described [here](../credible-set.md#explaining-l2g-predictions). These results feature as Target-Disease evidence, as well as L2G annotation for every credible in the Platform.&#x20;

{% hint style="info" %}
&#x20;The **GWAS Associations** evidence set is constructed based on GWAS credible sets linking to a protein-coding gene with an L2G score higher than 0.05.
{% endhint %}

### Reference

Mountjoy, E., Schmidt, E.M., Carmona, M. et al. [An open approach to systematically prioritize causal variants and genes at all published human GWAS trait-associated loci.](https://www.nature.com/articles/s41588-021-00945-5) Nat Genet 53, 1527–1533 (2021)
