# Colocalisation

Pairs of credible sets overlapping at least one variant are subject to additional analysis to infer the likelihood of them sharing the same causal variant. The Platform compares all GWAS vs all GWAS credible sets and all GWAS vs all molQTL credible sets. For overlapping credible sets, co-localisation metrics are estimated using the following methods:

## COLOC

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/coloc/)

If both overlapping credible sets are annotated with the logarithm of the Bayes factor (log(BF)), the Platform pipelines will estimate the probability of sharing the causal variant using the COLOC method ([Giambartolomei et al. , 2014](https://www.ncbi.nlm.nih.gov/pubmed/24830394)). COLOC uses Bayesian statistics to estimate posterior probabilities for the following hypothesis:

* **H0**: No association with either trait
* **H1**: Association with trait 1, not with trait 2
* **H2**: Association with trait 2, not with trait 1
* **H3**: Association with trait 1 and trait 2, two independent SNPs
* **H4**: Association with trait 1 and trait 2, one shared SNP

To reduce potential false positives in small overlaps, if the size of the overlap is less than 5 SNPs, we check whether the maximum product of the PIPs for at least one of the overlapping SNP pairs is greater than 0.01. Otherwise, the overlap is excluded from the COLOC analysis.

## eCAVIAR

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/ecaviar/)

If at least one credible sets in the overlap had no information about a variant log(BF), colocalisation analysis using eCAVIAR was performed. eCAVIAR is an a heuristic algorithm that uses SNP’s PIPs (see [Hormozdiari et al. (2016)](https://pubmed.ncbi.nlm.nih.gov/27866706/)) to estimate the colocalisation posterior probability (CLPP). CLPP is computed as the sum over the product of the variant fine-mapping probabilities between the two overlapping credible sets.

{% hint style="info" %}
**Credible set-based colocalisation**

All co-localisations presented in the Platform are based on credible sets. No estimates are based on full locus co-colocalisation
{% endhint %}
