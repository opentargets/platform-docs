# Fine-mapping

Fine-mapping is a statistical analysis technique used to pinpoint the specific genetic variant(s) most likely responsible for a trait association identified in a GWAS. The main result is a credible set (CS): the minimal list of variants with assigned posterior probabilities (PIPs) to be causal that form a predefined probability. The Platform uses 95% CS, meaning the CS has a 0.95 probability of containing the causal variant. The expected sum of PIPs for all variants in CSs have to be within the range of \[0.95,1].

**Open Targets Platform fine-mapping strategies (see more in** [**Fine-mapping pipelines**](fine-mapping.md#fine-mapping-pipelines)**):**

<table><thead><tr><th>Source</th><th>Clumping</th><th>Fine-mapping</th><th>LD</th><th data-type="rating" data-max="4">Confidence</th></tr></thead><tbody><tr><td><a href="data-sources.md#gwas-catalog-literature-curated-associations-gcca">GCCA</a></td><td><a href="fine-mapping.md#distance-based-clumping">Distance-based</a> + <a href="fine-mapping.md#ld-based-clumping">LD-based</a></td><td><a href="fine-mapping.md#pics-fine-mapping">PICS</a></td><td><a href="data-sources.md#ld-matrixes">gnomAD</a></td><td>1</td></tr><tr><td><a href="data-sources.md#gwas-catalog-summary-statistics-gcss">GCSS</a></td><td><a href="fine-mapping.md#distance-based-clumping">Distance-based </a>+ <a href="fine-mapping.md#ld-based-clumping">LD-based</a></td><td><a href="fine-mapping.md#pics-fine-mapping">PICS</a></td><td><a href="data-sources.md#ld-matrixes">gnomAD</a></td><td>2</td></tr><tr><td><a href="data-sources.md#gwas-catalog-summary-statistics-gcss">GCSS</a></td><td><a href="fine-mapping.md#locus-breaker">Locus breaker</a></td><td><a href="fine-mapping.md#susie-inf-fine-mapping">SuSiE-inf</a></td><td><a href="data-sources.md#pan-ukbb-ld-matrices">pan-UKBB</a></td><td>3</td></tr><tr><td><a href="data-sources.md#finngen">FinnGen</a></td><td>Study-specific</td><td>SuSiE</td><td>In-sample</td><td>4</td></tr><tr><td><a href="data-sources.md#eqtl-catalogue">eQTL catalogue</a></td><td>Study-specific</td><td>SuSiE</td><td>In-sample</td><td>4</td></tr><tr><td><a href="data-sources.md#the-pharma-proteomics-uk-biobank-project-ppp-ukbb">UKBB-PPP</a></td><td><a href="fine-mapping.md#locus-breaker">Locus breaker</a></td><td><a href="fine-mapping.md#susie-inf-fine-mapping">SuSiE-inf</a></td><td><a href="data-sources.md#pan-ukbb-ld-matrices">pan-UKBB</a></td><td>3</td></tr></tbody></table>

## Clumping

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/clumping/)

Clumping is a technique for selecting the most significant variants within a region or set of variants in LD, essentially collapsing signals into loci with an increased chance of containing a single causal variant for the phenotype. Three different methods are used for clumping:

### **Distance-based clumping**

The method is based on an iterative procedure in which the variant with the strongest p-value is selected and all other variants within a predefined distance (radius) from this variant are clumped together. The procedure is repeated as long as there is at least one significant variant. The output of the method is a list of lead variants. There are two parameters: the distance to clump and the p-value significance threshold.

### **LD-based clumping**

The method is applied to the results of the distance-based clumping (list of lead variants). It is again based on an iterative procedure in which the variant with the strongest p-value is selected and all other variants with high LD (r2>=0.5) are clumped together.&#x20;

### **Locus breaker**

The method consists of three steps:&#x20;

1. In the first step, we perform the regular distance-based clumping.
2. In the second step, we filter the input summary statistics by the baseline p-value (default is 1e-5). We then clump variants that are closer to each other than the cutoff distance (default is 250,000 bp). Next, we filter clumps by having at least one variant with a p-value above the genome-wide significance threshold. At this stage, we define a list of loci consisting of information about the lead variant and the locus boundaries (the leftmost and rightmost variants in the clump). To each of the locus boundaries we subtract/add (to the left/right boundaries respectively) the flanking distance (the default is 100,000 bp) to avoid situations where the locus size consisting of only one lead variant is 0.&#x20;
3. In the third step we select the loci with the size greater than the specified large locus size threshold (1,500,000 bp by default) and 'break' each of the large loci using the lead variants from the distance-based clump that lie within the boundaries of the large locus. For each of the distance-based lead variants, we assigned the boundaries as +/-half the size of the large locus size threshold. Thus, each large locus is divided by several overlapping loci of the size of the large locus size threshold. The small loci are unaffected by the splitting.&#x20;

The general procedure results in a list that contains information about the lead variant and the locus boundaries (the most left and right variants in the cluster), and the largest locus size doesn't exceed the large locus size threshold. The boundaries of the locus are then used to define the region for fine-mapping and LD matrix ingestion. The reason for using this procedure is because locus breaker results in smaller locus sizes on average compared to those defined by window-based clumping.

**Acknowledgements:** We are grateful to our colleagues at Human Technopole, Sodbo Sharapov and Nicola Pirastu, for advice on this method.

## PICS fine-mapping

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/pics/)

The PICS algorithm was originally implemented in [Farh et al. (2015)](https://www.nature.com/articles/nature13835) investigating the fine-mapping of causal autoimmune disease variants. It is a method to fine-map the most likely causal variants associated with a trait or disease within a haplotype. The algorithm is based on the calculation of the Posterior Inclusion Probabilities (PIP) of tag variants linked to the lead variant by LD within the target population. Only five populations are used for PICS fine-mapping: African-American (AFR), American Admixed/Latino (AMR), East Asian (EAS), Finnish (FIN), and Non-Finnish European (NFE). The calculation is performed by using all the proxy variants where r2 ≥ 0.5 and the default parameter k=6.4 as reported in the original paper.

## SuSiE-inf fine-mapping

📖 [Gentropy](https://opentargets.github.io/gentropy/python_api/methods/susie_inf/)

If both summary statistics and high-precision LD are available for the locus, we use SuSiE-inf  fine-mapping (see [Cui et al. (2024)](https://www.nature.com/articles/s41588-023-01597-3) for more details). This method is a generalisation of the original SuSiE, allowing modelling of infinitesimal effects alongside fewer larger causal effects.

SuSiE-inf has two approaches for updating estimates of the variance components: Method of Moments and Maximum Likelihood Estimator ('MoM' / 'MLE'). The function takes an array of Z-scores and a numpy array matrix of variant LD to perform fine-mapping. There is a boolean option “est\_tausq” that enables the estimation of infinitesimal effects. If it is disabled, it performs fine-mapping similar to the original SuSiE method. We use SuSiE-inf only with the combination of pan-UK Biobank LD matrices for three ancestries: NFE, CSA and AFR.

## Fine-mapping pipelines

Different pipeline strategies have been defined for different sources based on a combination of the above methodologies:

### **Clumping and fine-mapping of GCSS and GCCA PICS**

Distance and LD-based clumping is applied to all available GCSS and GCCA. P-value significance is defined at <=1e-8 threshold and distance-based clumping is performed using a 500,000 bp radius. LD-clumping is performed on the same window using the LD dataset from gnomAD v2.1.1. [PICS](fine-mapping.md#pics-fine-mapping) fine-mapping is then performed using the same LD information and credible sets are defined based on 95% inclusion probability. In the case of multiple ancestry studies, we used Non-Finnish Europeans (NFE) if it was in the list of ancestries, or major ancestry otherwise. In the case the study's ancestry is not in the list available in LD index ancestries, no fine-mapping results are produced. If the lead variant is not present in the LD-index, the credible set contains only that variant and it's flagged with the label `Variant not found in LD reference`. All resulting credible sets objects were additionally flagged with the label `Study locus fine-mapped without in-sample LD reference`.

### **Clumping and fine-mapping of GCSS SuSiE**

GWAS-significant study-locus are identified using a p-value threshold <=1e-8 and the [locus-breaker](fine-mapping.md#locus-breaker) method. [SuSiE-inf fine-mapping](fine-mapping.md#susie-inf-fine-mapping) was applied on all study-loci following the next criteria:

1. Major ancestry for the study is NFE, AFR, CSA or EAS. If the major ancestry was EAS, we used CSA instead
2. The study type is "gwas"
3. The study has no analysis flags except "metabolite"
4. Study has no quality control flags
5. The locus didn't overlap with the MHC region. We didn’t exclude X or Y chromosomes if they were presented in GWAS
6. The number of variants in the locus after overlapping with the LD matrix was in the range \[100, 15,000]

For all eligible study loci, the SuSiE-inf method was applied without estimation of infinitesimal effects (equivalent to the classical SuSiE method) using [pan-UKBB LD matrices](data-sources.md#pan-ukbb-ld-matrices). Filtering of the resulting 95% CSs is performed based on CS log(BF)<=2, minimum R2 purity <=0.25 and lead variant p-value>=1e-5. Additionally, the pairwise r^2 between lead variants within the locus is calculated, removing the less significant of the CSs if the r2>=0.8. As the locus breaker procedure can create overlapping loci, we can obtain the redundant credible sets within the same study. Thus, if two CSs from different loci within a study had the same lead variant, we removed one of them, leaving the CS with the largest CS log(BF). All resulting credible sets from this pipeline are flagged with the label `Study locus fine-mapped without in-sample LD reference`.

### UKBB-PPP clumping and fine-mapping

The [UKBB-PPP](data-sources.md#the-pharma-proteomics-uk-biobank-project-ppp-ukbb) summary statistics are clustered into locus using the [locus breaker](fine-mapping.md#locus-breaker) method using a p-value significance threshold <=1.7e-11. The resulting study-loci are fine-mapped using the [SuSiE-inf](fine-mapping.md#susie-inf-fine-mapping) method with [Pan-UKBB LD matrices](data-sources.md#pan-ukbb-ld-matrices) for the EUR population. The resulting 95% CSs are filtered similar to GCSS SuSiE pipeline described above. All resulting StudyLocus objects were additionally flagged with the label `Study locus fine-mapped without in-sample LD reference`.
