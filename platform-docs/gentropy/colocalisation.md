# Colocalisation

Pairs of credible sets overlapping at least one variant are subject to additional analysis to infer the likelihood of them sharing the same causal variant. The Platform compares all GWAS vs all GWAS credible sets and all GWAS vs all molQTL credible sets. For overlapping credible sets, colocalisation metrics are estimated using the following methods:

## COLOC-PIP

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/coloc_pip/)

COLOC-PIP is an adaptation of the COLOC method ([Giambartolomei et al. , 2014](https://www.ncbi.nlm.nih.gov/pubmed/24830394)), where instead of using log Bayes factors the H3 and H4 probabilities are calculated directly from the variant-level posterior inclusion probabilities. This means the method can be applied to credible sets with posterior probabilities derived from fine-mapping methods other than SuSiE. The method assumes the probabilities of H0, H1, and H2 are zero, as any overlap is already the result of two fine-mapped associations.&#x20;

* **H0**: No association with either trait
* **H1**: Association with trait 1, not with trait 2
* **H2**: Association with trait 2, not with trait 1
* **H3**: Association with trait 1 and trait 2, two independent SNPs
* **H4**: Association with trait 1 and trait 2, one shared SNP

## eCAVIAR

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/ecaviar/)

eCAVIAR is an a heuristic algorithm that uses SNP’s PIPs (see [Hormozdiari et al. (2016)](https://pubmed.ncbi.nlm.nih.gov/27866706/)) to estimate the colocalisation posterior probability (CLPP). CLPP is computed as the sum over the product of the variant fine-mapping probabilities between the two overlapping credible sets.

{% hint style="info" %}
**Credible set-based colocalisation**

All co-localisations presented in the Platform are based on credible sets. No estimates are based on full locus colocalisation
{% endhint %}
