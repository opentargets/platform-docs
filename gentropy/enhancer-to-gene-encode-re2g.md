# Enhancer-to-Gene (ENCODE rE2G)

Enhancer-to-gene scores are directly ingested from the ENCODE consortium, which utilises a mixture of epigenetic datasets to connect genomic regions (defined as chromosome, start, end) to putative genes. These regions are likely regulatory elements and affect the transcriptional activity of their annotated genes.

The input datasets are based on publicly available resources from the [ENCODE project](https://www.encodeproject.org/), these include&#x20;

* histone modification ChIP-seq,&#x20;
* open chromatin DNase-seq&#x20;
* ATAC-seq
* 3D chromatin conformation structure determined by Hi-C.&#x20;

These inputs are normalised and used as features in a machine learning approach described in the [original rE2G publication](https://www.biorxiv.org/content/10.1101/2023.11.09.563812v1).  The final output connects potential regulatory regions to their target genes, along with a score that ranges between 0 to 1 that indicates the confidence of a given assignment.

### rE2G in the platform

Enhancer-to-gene scores from rE2G are ingested into the Open Targets ecosystem through the orchestration and can be&#x20;

* browsed through the variant page, where the regulatory regions overlapping a given variant of interest are displayed in the enhancer-to-gene widget. &#x20;
* browsed through the credible set page, which shows the overlapping rE2G scores for the lead variant of the credible set.
* viewed in the form of `e2gMean` and `e2gNeighbourhoodMean` features in the L2G predictions.

### Applied transformations

The dataset is downloaded in the latest version using the ENCODE API and transformed to the [Interval](https://opentargets.github.io/gentropy/python_api/datasets/intervals/) gentropy format. The mapping between original biosamples provided by the source was based on [manual curation](https://github.com/opentargets/curation/blob/25.12.2/genetics/E2G_biosample_mapping.csv). We apply post-transformation quality controls and flagging system that includes:

* Validation of gene identifiers from input against latest Ensembl version&#x20;
* Validation of biosample identifiers against the latest Biosample dataset
* Score stringent filtering

We have implemented a stringent filter of 0.6 on the rE2G dataset to reduce computational costs and redundancy.  The selection of the filter was based on an analysis performed on rE2G overlaps with eQTL credible sets.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p><strong>Effect of rE2G-score filtering on gene prioritisation for eQTL credible sets.</strong><br>True positives are defined as the eQTL target gene; <strong>Sensitivity</strong> (orange) is TP recall, and <strong>FDR</strong> (blue) = 1 − precision among retained cs–gene pairs. Points are thresholds labelled by percentiles (Px) of the <strong>rE2G score</strong> distribution. <strong>Moderate filtering</strong> removes significant amounts of raw rE2G entries while <strong>retaining most TP assignments</strong>. <strong>FDR changes little until very aggressive cutoffs</strong>, indicating many non-TP—but potentially interesting—gene links persist.</p></figcaption></figure>

