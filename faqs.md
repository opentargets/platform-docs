# 🆕 FAQs

**Do you have questions or comments for us? Ask on** [**Open Targets Community**](https://community.opentargets.org/c/frequently-asked-questions/6)**!**



* **Why can't I find a variant that I search for?**&#x20;

In the Open Targets Platform, a variant refers to any human variation that is associated with a [disease, trait or phenotype](disease-or-phenotype/) that has been reported in at least one of our [variant-to-phenotype](variant.md#variant-to-phenotype) sources. This accounts for only 1% of the total variants reported in [gnomAD](https://gnomad.broadinstitute.org/) (6.5M vs 700M). See [here](variant.md) for more information.



* **Why can't I find a study I search for?**

Each [study](https://app.gitbook.com/o/-LC3OlEMulAutIN2QOro/s/-MU4dMxOmLaVNWfVNvpC/~/changes/506/study) undergoes quality control and validation procedures before ingestion into the Platform.&#x20;

We remove studies that had unsupported study types, invalid target ID or invalid biosample ID (for molQTLs), and invalid ontology trait mapping. See [here ](https://app.gitbook.com/o/-LC3OlEMulAutIN2QOro/s/-MU4dMxOmLaVNWfVNvpC/~/changes/506/study#study-inclusion-criteria)for study inclusion criteria.

For GWAS Catalog studies with summary statistic, we perform [summary statistic quality control](gentropy/data-sources.md#gcss-quality-control). If this fails, we exclude it.

&#x20;For GWAS Catalog curated associations (top hits), we tightened the p-value significance threshold compared to OTG 22.10 (1e-8 instead of 5e-8). This may also lead to differences in the study list.



* **What is a Credible Set?**

A credible set is the set of variants near a genetic association signal that have a 95% probability of containing the true causal variant(s) for that signal.



* **What are the quality control criteria for fine mapping?**

Credible sets (CSs) are filtered out based on the following criteria:

1. The lead variant maps within the MHC region (`chr6:25726063-33400556`)
2. The lead variant has invalid chromosome coding (`1:22, X, Y, XY, mt`)
3. The CS is not on the list of valid studies
4. It is the GWAS Catalog Summary Statistics PICS CSs and it has valid SuSiE CS from the same region and study
5. It is the GWAS Catalog Curated Association PICS CS and it has valid GWAS Catalog Summary Statistics PICS CS from the same region and study
6. The sum of PIPs in the CS is not within the \[0.95, 1] range
7. The CS didn't pass the study-specific p-value threshold (e.g. GWAS Catalog Curated Association p-value<=1e-8)



* **Why is the V2G score not available anymore?**

The variant-to-gene (V2G) score was developed as an aggregated score for the assignment of the variant to the gene in the region using different sources, such as association with molQTLs and VEP. &#x20;

Although intuitive, V2G does not reflect the complexity of modern data.&#x20;

We have therefore introduced a new score - [Locus-to-Gene score (L2G)](gentropy/locus-to-gene-l2g.md), based on a machine learning algorithm that assesses the assignment score of the credible set (not only variant) to gene and does not use the old V2G pipeline anymore. It is a more accurate and sophisticated way of assigning genes to associated GWAS loci. In some cases, the L2G could be interpreted as V2G if the credible set is the size of only one variant. In the new Platform datasets, the L2G score has completely superseded V2G.

Full information about variant assignment to genes based on distance or VEP is available on all [variant ](variant.md)pages in the corresponding widgets. There is also information about whether the variant is part of the molQTL credible set, which can also be used to assign this variant to the gene of interest (available in the molQTL widget).&#x20;



* **Why are some L2G associations I found in OT Genetics 22.10 not found in the L2G predictions in OT Platform 25.03?** &#x20;

There could be several reasons for this:

1. We don't have the matching study anymore (due to quality control or validation).
2. We don't have the corresponding credible set anymore due to a different fine-mapping approach or p-value filtering thresholds (e.g. for GWAS Catalog curated associations we now use p-value < 1e-8 instead of p-value < 5e-8 in OTG 22.10).
3. The L2G model is different and can lead to different L2G estimates even when the same study and variant are presented. We don't display L2G assignments when L2G < 0.05.



* **Where can I find studies or credible sets excluded from the Platform?**

To ensure high-quality outputs, the data processing pipelines perform a number of validation steps across different datasets. For data provenance considerations the excluded part of the datasets are also available both on FTP (`ftp://ftp.ebi.ac.uk/pub/databases/opentargets/platform/{release}/excluded`) and Google Cloud (`gs://open-targets-data-releases/{release}/excluded/`). In this folder you'll find the list of excluded credible sets (`credible_set`), evidence (`evidence`), interactions (`interaction`), studies (`study`) and target validation (`target_validation`) dataset. These datasets also provide context about the reason for exclusion.
