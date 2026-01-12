# Target–disease evidence

## Target–disease evidence

Every event or set of events pinpointing a target as a potential causal gene or protein for a disease represents the unit of information, most often referred to as **evidence**. Within the Open Targets Platform, a series of pipelines ensure information is retrieved from its sources and standardised in a way that can be immediately applied to answer drug development queries.

All evidence is mapped to the reference target entity identifier (Ensembl gene) and disease or phenotype identifier (experimental factor ontology, EFO), as well as other reference controlled vocabularies and ontologies when appropriate. Evidence is also reviewed to minimise the presence of duplicates within the same data source.

Data sources are also grouped into bigger categories abstracting the type of evidence they predominantly capture. In the platform, these categories are usually referred to as data types, as opposed to the individual resource data referred to as **data sources**.

The Open Targets Platform provides a scoring framework for each data source to contextualise the relative importance of each piece of evidence. This score will be more relevant when understanding the association scoring in later sections.

## Evidence data sources

### GWAS associations

The GWAS associations data source aggregates target-disease relationships supported by significant genome-wide associations (GWAS) in the context of other functional genomics data.

The evidence in this data source results from a comprehensive statistical genetics analysis described in [GWAS and functional genomics](gentropy/) section. The aim of this analysis is to identify GWAS-significant signals across an [extensive set](gentropy/data-sources.md) of GWAS studies covering binary and quantitative traits. To address linkage disequilibrium, all significant signals are [fine-mapped](gentropy/fine-mapping.md) and the resulting credible sets [colocalised](credible-set.md#colocalisation) against molQTL studies. All GWAS and functional genomic features are leveraged by the [Locus-to-Gene](gentropy/locus-to-gene-l2g.md) machine-learning method aimed to prioritise likely causal genes in the region.

The GWAS association evidence is defined as any credible set in a GWAS trait associated with a gene with a Locus2Gene (L2G) > 0.05. The feature contributions for the L2G predictions are also [explained](credible-set.md#explaining-l2g-predictions) by SHAP analysis helping with the interpretation of the observed features. All credible sets can also be futher interrogated in their own [credible set](credible-set.md) page, including an interpretation of the directionality in the context of colocalising molQTL studies.

**Data type**: Genetic association

**Evidence scoring**: [Locus-to-Gene score](gentropy/locus-to-gene-l2g.md), filtered to use scores above 0.05



### Gene Burden

Gene burden data comprises gene–phenotype relationships observed in gene-level association tests using rare variant collapsing analyses. The Platform integrates burden tests carried out by several sources:

* **REGENERON** (Backman et al., 2021), a whole-exome sequencing analysis of individuals from the UK Biobank.
* **AstraZeneca PheWAS Portal** (Wang et al., 2021), a whole-exome sequencing analysis of individuals from the UK Biobank.
* **Genebass** (Karczewski et al., 2022): Gene-based Association Summary Statistics (Genebass),  a whole-exome sequencing analysis of individuals from the UK Biobank.
* The results of whole-exome and whole-genome sequencing analysis based on the **SPARK cohort** bring evidence of novel targets implicated in **autism spectrum disorder** (Zhou et al., 2022).
* **The SCHEMA consortium** (Singh et al., 2022), a whole-exome sequencing analysis of individuals with **schizophrenia**.
* **The Epi25 collaborative** (Epi25 Collaborative, 2019), a whole-exome sequencing analysis of individuals with **epilepsy**.
* **The Autism Sequencing Consortium** (Satterstrom et al., 2020), a whole-exome sequencing analysis of individuals with **autism spectrum disorder.**
* The results of an **Open Targets project** (Bomba et al., 2022), a whole-exome sequencing analysis of individuals from the INTERVAL cohort testing for associations between rare coding variants and **blood metabolites**.
* The results of a pan-ancestry whole-exome sequencing analysis identify relevant genes associated with **fat distribution** (Akbari et al., 2022).
* The results of whole-exome and whole-genome sequencing analysis on **Parkinson disease** and promoted by the **AMP-PD initiative**, and other collaborators (Makarious et al., 2022).
* The results of gene-based analyses of rare variants and circulating metabolic biomarkers relevant to **cardiovascular disease** (Riveros-McKay et al., 2020).
* The results of rare coding variant analyses from whole exome sequencing of Black South African men to identify genes significantly associated with **prostate cancer** (Soh et al., 2023)
* The **FinnGen (R12)** gene-based burden test results from collapsing loss of function variants, based on **genotyping** data from the Finnish population. [Find out more in their documentation](https://finngen.gitbook.io/documentation/methods/lof-variant-burden).
* The **Broad CVDI Human Disease Portal** is a pan-ancestry whole-exome and whole-genome sequencing analysis combining data from three major biobanks: the **UK Biobank**, **All of Us**, and the **Mass General Brigham Biobank**. This comprehensive study analysed rare variant associations across nearly 750,000 individuals, identifying 363 significant gene-disease associations for 123 genes across 165 diseases. The analysis includes both cohort-specific burden tests and meta-analyses across ancestries (Jurgens et al., 2024).

These associations are a result of collapsing rare variants in a gene into a single burden statistic and regress the phenotype on the burden statistic to test for the combined effects of all rare variants in that gene. The different collapsing methods inform about the filters used to select the set of qualifying variants, mostly based on their pathogenicity and frequency in the population.

**Data type**: Genetic association

**Evidence scoring:** Scaled p-value from 0.25 (p = 1e-7) to 1 (p < 1e-17).

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th width="331" align="center">Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th align="center">Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td align="center">Assumption of all variants LoF</td><td align="center">2Amved8pXoFQ-Vl4kLr3A1X6R</td></tr></tbody></table>

**Source:** [AstraZeneca PheWAS Portal](https://azphewas.com), [Genebass](https://app.genebass.org)

**References:** [Wang, Q. et al, 2021](https://doi.org/10.1038/s41586-021-03855-y); [Backman, J.D. et al, 2021](https://doi.org/10.1038/s41586-021-04103-z); [K.K., Karczewski et al., 2022](https://www.medrxiv.org/content/10.1101/2021.06.19.21259117v4); [Zhou X. et al, 2022](https://www.nature.com/articles/s41588-022-01148-2), [Singh et al., 2022](https://rdcu.be/cPZP3); [Epi25 Collaborative, 2019](https://www.cell.com/ajhg/fulltext/S0002-9297\(19\)30207-1); [Satterstrom et al., 2020](https://www.sciencedirect.com/science/article/pii/S0092867419313984); [Bomba et al., 2022](https://www.cell.com/ajhg/fulltext/S0002-9297\(22\)00157-4); [Akbari, P., 2022](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9399235/); [Makarious et al., 2022](https://www.medrxiv.org/content/10.1101/2022.11.08.22280168v1.full.pdf); [Riveros-McKay et al., 2020](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1008605); [Soh et al., 2023](https://doi.org/10.1038/s41467-023-43726-w); [Jurgens et al., 2024](https://doi.org/10.1038/s41588-024-01894-5)



### ClinVar

ClinVar is an NIH public archive of reports of the relationships among human variations and phenotypes, with supporting evidence. The ClinVar data source in the Open Targets Platform captures the subset of ClinVar that refers to germline variants (as opposed to somatic variants). Each evidence in the platform aims to capture an individual RCV record in ClinVar.

Information on variants is covered extensively for both single point and structural variants. When available, genomic coordinates are reported with RS numbers, or by following the CHROM\_POS\_REF\_ALT and HGVS notations.

**Data type**: Genetic association

**Evidence scoring**: ClinVar evidence is scored in a 2-step process. In Step 1, a score is assigned to every piece of evidence based on the clinical significance:

| Clinical significance                        | Evidence score |
| -------------------------------------------- | -------------- |
| association not found                        | 0              |
| benign                                       | 0              |
| not provided                                 | 0              |
| likely benign                                | 0              |
| conflicting data from submitters             | 0.3            |
| conflicting interpretations of pathogenicity | 0.3            |
| low penetrance                               | 0.3            |
| other                                        | 0.3            |
| uncertain risk allele                        | 0.3            |
| uncertain significance                       | 0.3            |
| established risk allele                      | 0.5            |
| risk factor                                  | 0.5            |
| affects                                      | 0.5            |
| likely pathogenic                            | 0.7            |
| association                                  | 0.9            |
| confers sensitivity                          | 0.9            |
| drug response                                | 0.9            |
| protective                                   | 0.9            |
| pathogenic                                   | 0.9            |

In Step 2, the score is modulated based on the ClinVar review status:

| Confidence                                           | Evidence score modifier |
| ---------------------------------------------------- | ----------------------- |
| no assertion provided                                | +0                      |
| no assertion criteria provided                       | +0                      |
| no assertion for the individual variant              | +0                      |
| criteria provided, single submitter                  | +0.02                   |
| criteria provided, conflicting interpretations       | +0.02                   |
| criteria provided, multiple submitters, no conflicts | +0.05                   |
| reviewed by expert panel                             | +0.07                   |
| practice guideline                                   | +0.1                    |

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th align="center">Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th align="center">Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td align="center">LoF variants</td><td align="center">2Amved8pXoFQ-Vl4kLr3A1X6R</td></tr></tbody></table>

**Source**: [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/) (via [European Variation Archive](https://www.ebi.ac.uk/eva/))

**References**: [Cezard T. et al, 2021](https://doi.org/10.1093/nar/gkab960); [Shen A. et al, 2024](https://doi.org/10.1093/bioadv/vbae018); [Landrum, M. et al, 2014](https://doi.org/10.1093/nar/gkt1113); [Landrum, M. et al, 2020](https://doi.org/10.1093/nar/gkz972)



### Genomics England (GEL) PanelApp

The Genomics England PanelApp is a knowledge base that combines crowdsourced expertise with curation to provide gene–disease relationships. Virtual gene panels related to human disorders are reviewed by experts within the clinical and scientific community to support the interpretation of genomes within the 100,000 Genomes Project. Within a panel, genes are rated based on the level of evidence supporting the association with the phenotypes identified by the panel. Genes are then classified according to a traffic light system with red/stop, amber/pause, and green/go classifications. To receive a green rating (diagnostic-grade) on a version 1+ panel, the gene requires "evidence from 3 or more unrelated families or from 2-3 unrelated families where there is strong additional functional data" and "genes that do not meet these criteria are rated as Amber (borderline) or Red (low level of evidence)."

The Open Targets Platform includes "green" and "amber" genes from version 1+ panels along with their phenotypes, providing the latter can be mapped to a disease or phenotype ontology. As we standardise our evidence to EFO, some of the phenotypes cannot be mapped and included in the Platform; please visit the [Genomics England PanelApp website](https://panelapp.genomicsengland.co.uk) for the full set.

**Data type**: Genetic association

**Evidence scoring**: Based on Genomics England gene rating:

| Gene Rating in GEL Panel | Evidence score |
| ------------------------ | -------------- |
| Amber                    | 0.5            |
| Green                    | 1              |

**Source**: [Genomics England PanelApp](https://panelapp.genomicsengland.co.uk)

**References**: [Martin, A. et al, 2019](https://doi.org/10.1038/s41588-019-0528-2)



### Gene2Phenotype

The data in Gene2Phenotype (G2P) is produced and curated from the literature by different sets of panels formed by consultant clinical geneticists. The G2P data is designed to facilitate the development, validation, curation, and distribution of large-scale, evidence-based datasets for use in diagnostic variant filtering. Each G2P entry associates an allelic requirement and a mutational consequence at a defined locus with a disease entity. A confidence level and evidence link are assigned to each entry. This confidence level follows the terminology described by [GenCC](https://thegencc.org/about.html) for describing gene–disease validity.

G2P evidence in the Platform is the result of any target-disease curation by any of the expert panels.

**Data type:** Genetic association

**Evidence scoring:**

| Gene2Phenotype confidence | Evidence score |
| ------------------------- | -------------- |
| Limited                   | 0.01           |
| Moderate                  | 0.5            |
| Strong                    | 1              |
| Both RD and IF            | 1              |
| Definitive                | 1              |

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th>Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th>Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td>LoF and GoF variants</td><td>Assumption of Risk</td></tr></tbody></table>

**Source**: [Gene2Phenotype](https://www.ebi.ac.uk/gene2phenotype)

**References**: [Thormann, A. et al, 2019](https://doi.org/10.1038/s41467-019-10016-3)



### UniProt literature

The Universal Protein Resource (UniProt) provides a large compendium of sequence and functional information at the protein level. As part of their functional annotation effort, UniProt curators also annotate proteins with publications supporting their involvement on pathogenic processes.

All publications supporting a given target disease relationship are aggregated into one single Platform evidence.

**Data type**: Genetic association

**Evidence scoring**:&#x20;

| **Uniprot confidence** | Evidence score |
| ---------------------- | -------------- |
| Medium                 | 0.5            |
| High                   | 1              |

**Source**: [UniProt](https://www.uniprot.org)

**References**: [The UniProt Consortium, 2021](https://academic.oup.com/nar/article/49/D1/D480/6006196)



### UniProt curated variants

The Universal Protein Resource (UniProt) also curate variants supported by publications that are known to alter protein function on disease. Curated mutations are predominantly protein coding or in regulatory regions clearly associated with the causal protein.

All publications supporting a given variant in connection with a disease constitute individual evidence. All supporting publications are aggregated within the same evidence.

**Data type**: Genetic association

**Evidence scoring**:&#x20;

| **UniProt confidence** | Evidence score |
| ---------------------- | -------------- |
| Medium                 | 0.5            |
| High                   | 1              |

**Source**: [UniProt](https://www.uniprot.org)

**References**: [The UniProt Consortium, 2021](https://academic.oup.com/nar/article/49/D1/D480/6006196)



### Orphanet

Orphanet is an international network that offers a range of resources to improve the understanding of rare disorders of genetic origin. These resources include an inventory of rare disease and gene associations, classification of the gene–disease relationship, information on the kind of mutation, and supporting publication references.

**Data type**: Genetic association

**Evidence scoring:**

| Orphanet Disorder Gene Association Status | Evidence score |
| ----------------------------------------- | -------------- |
| Not yet assessed                          | 0.5            |
| Assessed                                  | 1              |

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th>Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th>Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td>LoF and GoF variants</td><td>Assumption of Risk</td></tr></tbody></table>

**Source**: [Orphanet Genes Associated with Rare Diseases](https://www.orpha.net/consor/cgi-bin/Disease_Genes.php?lng=EN)

**References**: [Orphanet](https://www.orpha.net); [Orphadata](http://www.orphadata.org/cgi-bin/index.php)



### ClinGen

The Clinical Genome Resource (ClinGen) Gene–Disease Validity Curation aims to evaluate the strength of evidence supporting or refuting a claim that variation in a particular gene causes a particular disease. ClinGen provides a framework of guidelines to assess clinical validity in a semi-quantitative manner allowing curators to classify the validity of given gene–disease pair.

All gene–disease pairs mapped to EFO constitute individual evidence in the Platform.

**Data type**: Genetic association

**Evidence scoring:**

| **ClinGen classification** | Evidence score |
| -------------------------- | -------------- |
| No reported evidence       | 0.01           |
| Refuted                    | 0.01           |
| Disputed                   | 0.01           |
| Limited                    | 0.01           |
| Moderate                   | 0.5            |
| Strong                     | 1              |
| Definitive                 | 1              |

**Source**: [ClinGen Gene-Disease Validity](https://clinicalgenome.org/curation-activities/gene-disease-validity/)

**References**: [Strande, N. et al., 2017](https://doi.org/10.1016/j.ajhg.2017.04.015)



### **Cancer Gene Census**

Cancer Gene Census (CGC) is part of the Wellcome Sanger Institute Catalogue of Somatic Mutations in Cancer ([COSMIC](http://cancer.sanger.ac.uk/cosmic)). CGC is an effort to catalogue genes which contain mutations that have been causally implicated in cancer. The exhaustive curation of the CGC covers individual studies as well as pan-cancer sequencing efforts, including The Cancer Genome Atlas (TCGA) and the International Cancer Genome Consortium (ICGC) among others.

In the Platform, CGC evidence is aggregated at the target–disease level to provide a summary of all curated evidence supporting the involvement of a target with a particular cancer type.

**Data type**: Somatic mutations

**Evidence scoring**: Scoring is based on the [Cancer Gene Census tier system](https://cancer.sanger.ac.uk/census)

| Modulator | Condition                                                                                         |
| --------- | ------------------------------------------------------------------------------------------------- |
| -0.25     | Only 1 mutated sample                                                                             |
| +0.25     | Gene mutated more frequently in particular disease compared to other diseases                     |
| +0.25     | Mutations in gene occur more frequently than in other genes of similar length in the same disease |

**Source**: [Cancer Gene Census](https://cancer.sanger.ac.uk/census)

**References**: [Sondka, Z. et al, 2018](https://doi.org/10.1038/s41568-018-0060-1)



### **IntOGen**

IntOGen provides a framework to identify potential cancer driver genes using large-scale mutational data from sequenced tumour samples. By harmonising tumour sequencing data from the ICGC/TCGA Pan-Cancer Analysis of Whole Genomes ([PCAWG](https://dcc.icgc.org/pcawg)) and other comprehensive efforts, IntOGen aims to provide a consensus assessment of cancer driver genes. Several state-of-the-art driver methodologies aiming to cover different approaches (e.g. dN/dS, Hotspots, etc.) are included to finally produce a consensus q-value for each driver gene in every tumour.

In the Platform, independent target–disease evidence are defined as any significant driver gene detected in any individual cohort. Information regarding the individual driver methods is also provided within each evidence.

**Data type**: Somatic mutations

**Evidence scoring**: Scaled [combined q-values](https://intogen.readthedocs.io/en/latest/drivers_combination.html) from 0.25 (q = 0.1) to 1 (q < 1e-10)

**Source**: [intOGen](http://www.intogen.org/search)

**References**: [Martínez-Jiménez, F. et al, 2020](https://doi.org/10.1038/s41568-020-0290-x)



### **ClinVar (somatic)**

ClinVar is an NIH public archive of reports of the relationships among human variations and phenotypes, with supporting evidence. The ClinVar (somatic) data source in the Open Targets Platform captures the subset of ClinVar that refers to somatic variants (as opposed to germline variants).

Information on variants is covered extensively for both single point and structural variants. When available, genomic coordinates are reported with RS numbers, or by following the CHROM\_POS\_REF\_ALT and HGVS notations. &#x20;

Each evidence in the Platform aims to capture an individual RCV record in ClinVar.

**Data type**: Somatic mutations

**Evidence scoring**: ClinVar evidence is scored in a 2-step process. In Step 1, a score is assigned to every piece of evidence based on the clinical significance:

| Clinical significance                        | Evidence score |
| -------------------------------------------- | -------------- |
| association not found                        | 0              |
| benign                                       | 0              |
| not provided                                 | 0              |
| likely benign                                | 0              |
| conflicting interpretations of pathogenicity | 0.3            |
| other                                        | 0.3            |
| uncertain significance                       | 0.3            |
| risk factor                                  | 0.5            |
| affects                                      | 0.5            |
| likely pathogenic                            | 0.7            |
| association                                  | 0.9            |
| drug response                                | 0.9            |
| protective                                   | 0.9            |
| pathogenic                                   | 0.9            |

In Step 2, scored is modulated based on the ClinVar review status:

| Confidence                                           | Evidence score modifier |
| ---------------------------------------------------- | ----------------------- |
| no assertion provided                                | +0                      |
| no assertion criteria provided                       | +0                      |
| no assertion for the individual variant              | +0                      |
| criteria provided, single submitter                  | +0.02                   |
| criteria provided, conflicting interpretations       | +0.02                   |
| criteria provided, multiple submitters, no conflicts | +0.05                   |
| reviewed by expert panel                             | +0.07                   |
| practice guideline                                   | +0.1                    |

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th align="center">Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th align="center">Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td align="center">LoF variants</td><td align="center">2Amved8pXoFQ-Vl4kLr3A1X6R</td></tr></tbody></table>

**Source**: [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/) (via [European Variation Archive](https://www.ebi.ac.uk/eva/))

**References**: [Cezard T. et al, 2021](https://doi.org/10.1093/nar/gkab960); [Shen A. et al, 2024](https://doi.org/10.1093/bioadv/vbae018); [Landrum, M. et al, 2014](https://doi.org/10.1093/nar/gkt1113); [Landrum, M. et al, 2020](https://doi.org/10.1093/nar/gkz972)



### Cancer Biomarkers

One of the aims of the Cancer Genome Interpreter is to identify how variations in the tumour genome may influence its response to anti-cancer therapies. The Cancer Biomarkers database features biomarkers of drug sensitivity, resistance, and toxicity for drugs targeting specific targets in cancer, curated by clinical and scientific experts in precision oncology, and classified by cancer type.

**Data type:** Somatic mutations

**Evidence scoring:** All manually curated evidence in Cancer Biomarkers has a score of 1

**Source:** [Cancer Genome Interpreter](https://www.cancergenomeinterpreter.org/biomarkers)

**References:** [Tamborero, D. et al, 2018](https://genomemedicine.biomedcentral.com/articles/10.1186/s13073-018-0531-8)



### ChEMBL

EMBL-EBI's ChEMBL is a manually curated database of bioactive molecules with drug-like properties, either approved for marketing by the U.S Food and Drug Administration (FDA), or clinical candidates. ChEMBL also captures information regarding the drug molecule indications, as well as their curated pharmacological target.

In the Platform, ChEMBL evidence represents any target–disease relationship that can be explained by an approved or clinical candidate drug, targeting the gene product and indicated for the disease. Independent studies are treated as individual evidence.

To provide additional context, we integrate a machine learning-based analysis of the reasons why a clinical trial has ended earlier than scheduled. This sorts the stop reasons into a set of 17 classes which include negative, neutral, and positive reasons. This information is available when hovering on the tooltip of the Source column.

The 17 classes are: Another Study, Business or Administrative, Negative, Study Design, Invalid Reason, Ethical Reason, Insufficient Data, Insufficient Enrolment, Study Staff Moved, Endpoint Met, Regulatory, Logistics or Resources, Safety and Side Effects, No Context, Success, Interim Analysis, and Covid 19.&#x20;

**Data type**: Known drug

**Evidence scoring:** ChEMBL evidence is scored in a 2-step process. In Step 1, a score is assigned to every piece of evidence based on the clinical precedence:

| Clinical Precedence                      | Evidence score |
| ---------------------------------------- | -------------- |
| Phase I (Early)                          | 0.05           |
| Phase I                                  | 0.1            |
| Phase II                                 | 0.2            |
| Phase III                                | 0.7            |
| Phase IV (only for approved indications) | 1              |

In Step 2, for those clinical trials that have stopped early, the score is down-weighted based on the classification of the reason to stop. In this way, less importance is attributed to evidence of studies that have been stopped due to negative outcomes or safety concerns:

| Reason to stop class   | Score weight |
| ---------------------- | ------------ |
| Negative               | 0.5          |
| Safety or side effects | 0.5          |

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th align="center">Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th align="center">Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td align="center">2Amved8pXoFQ-Vl4kLr3A1X6R</td><td align="center">Assumption of Protective</td></tr></tbody></table>

**Source**: [ChEMBL](https://www.ebi.ac.uk/chembl/)

**References**: [Mendez, D. et al, 2019](https://academic.oup.com/nar/article/47/D1/D930/5162468)



### CRISPR screens

One of the most powerful approaches to uncover gene function is the experimental perturbation of genes followed by the observation of related phenotypes. The perturbation of gene function in human cells has been greatly facilitated by developments in CRISPR technology.

CRISPRbrain is a database for functional genomics screens in differentiated human brain cell types. We have prioritised genome-wide [CRISPRi/a/KO screens](https://crisprbrain.org/background/) (healthy vs KO) for integration in the Platform to generate target–disease evidence.

We have linked cell types to diseases, meaning these diseases are often characterised with abnormal phenotypes in these cell types — hence the association.\
If knocking out a gene causes significant perturbation in the cell type, it might indicate a potential targeting strategy in the disease.

**Data type**: Affected pathway

**Evidence Scoring**: The Platform uses the linearised CRISPRbrain's assessment of statistical significance to assign a score, including hits from both the upper and lower end of the distribution

**Source**: [CRISPRbrain](https://crisprbrain.org/)&#x20;

**Reference**: [Tian, R et al, 2021](https://www.nature.com/articles/s41593-021-00862-0)



### Project Score

Project Score is a Wellcome Sanger Institute resource that aims to identify dependencies in cancer cell lines to guide precision medicine. The project combines gene fitness effects derived from whole-genome CRISPR-Cas9 synthetic lethality screenings with tractability data, genomic biomarkers and various target annotation enabling a systematic prioritisation of potential targets. The resulting inferences are then mapped from the cancer cell lines in which the experiment is performed to their corresponding tumours.&#x20;

In the Platform, any Project Score prioritised target with priority score reaching 36.0 is included as independent evidence; however, pan-cancer dependencies are excluded from the integration.

**Data type**: Affected pathway

**Evidence scoring**: Project Score priority score divided by 100

**Source**: CRISPR (via[ Project Score](https://score.depmap.sanger.ac.uk))

**References**: [Pacini et al, 2024](https://pubmed.ncbi.nlm.nih.gov/38215750/)



### SLAPenrich

SLAPenrich (Sample-population Level Analysis of Pathway enrichments) is a novel statistical framework for the identification of significantly mutated pathways, at the sample population level, in large cohorts of cancer patients. SLAPenrich is based on a Poisson binomial model that takes into account the length of blocks of exons in genes within each pathway, and the background mutation rate of the analysed cohort of patients. SLAPenrich enrichment analysis is based on EMBL-EBI Reactome pathways and mutation data from The Cancer Genome Atlas ([TCGA](https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga)) cohort.

In the Platform, each pathway significantly enriched in tumour-occurring mutations constitutes an individual piece of evidence.

**Data type**: Affected pathway

**Evidence scoring**: Scaled enrichment p-value from 0.5 (p = 1e-4) to 1 (p<1e-14).

**Source**: [SLAPenrich](https://saezlab.github.io/SLAPenrich/)

**References**: [Iorio, F. et al, 2018](https://doi.org/10.1038/s41598-018-25076-6)



### PROGENy

PROGENy (Pathway RespOnsive GENes) is a linear regression model that calculates pathway activity estimates based on consensus transcriptomic gene signatures obtained from perturbation experiments. PROGENy ([Schubert et al](https://www.nature.com/articles/s41467-017-02391-6.epdf?author_access_token=16QkzhJ3OA3qJDqBw_GvGdRgN0jAjWel9jnR3ZoTv0NBFLUVI-ebH2AmtFlR1ykSPIho7ETJXL7VqZFC4zGtU0BaeoZncGrwx3ZW24lfVqvbSWqsQKaUXFTi_c-4pgcpX-1qerWYlkG6sha8rhrnMg%3D%3D)) provides a framework to systematically compare pathway activities between normal and primary samples from The Cancer Genome Atlas (TCGA).

In the Platform, a PROGENy evidence is defined as any significantly regulated sample-level pathway activities inferred from matched normal vs. tumour samples.

**Data type**: Affected pathway

**Evidence scoring**: Scaled p-value from 0.5 (p = 1e-4) to 1 (p<1e-14).

**Source**: [PROGENy](https://saezlab.github.io/progeny/)

**References**: [Schubert, M. et al, 2018](https://doi.org/10.1038/s41467-017-02391-6)



### Reactome

The Reactome database manually curates and identifies reaction pathways that are affected by a disease. Reactome annotation includes information regarding the causal target–disease link either being a protein coding mutation or an altered expression.

In the Platform, any mutation or altered expression event affecting a different reaction is captured in a different target–disease evidence.

**Data type**: Affected pathway

**Evidence scoring**: All manually curated evidence in Reactome has a score of 1.

**Source**: [Reactome](https://reactome.org)

**References**: [Jassal, B. et al, 2020](http://doi.org/10.1093/nar/gkz1031)



### Gene signatures

The Platform also provides information about key driver genes for specific diseases that have been curated from Systems Biology analysis. These publications present different disease gene signatures as potential key drivers or key regulators causing disease.

**Data type**: Affected pathway

**Evidence scoring**: Scoring depends on whether the original data contains or not a score:

* p-values and rank-based scores are normalised to the 0.5 - 1 range
* If there is no score a fixed value of 0.5 is used

**References**: [Peters, L. A. et al, 2017](https://doi.org/10.1038/ng.3947); [Huan, T. et al, 2013](https://doi.org/10.1161/atvbaha.112.300112); [Zhang, B. et al, 2013](https://doi.org/10.1016/j.cell.2013.03.030); [Mostafavi, S. et al, 2018](https://doi.org/10.1038/s41593-018-0154-9)



### **Europe PMC**

The EMBL-EBI's Europe PMC enables access to a worldwide collection of life science publications and preprints from trusted sources. The Europe PMC data source aims to identify target–disease co-occurrences in the literature and provide an assessment on the confidence of the relationship. This pipeline uses deep-learning based Named Entity Recognition (NER) to identify gene/proteins and diseases when mentioned in the text, to later normalise them to the target or disease/phenotype entities in the Platform. All co-occurrences of both types of entities in the same sentence are considered evidence.

In the Platform, a piece of Europe PMC evidence is the result of aggregating all co-occurrences of the same target and disease within the same publication.

**Data type**: Literature

**Evidence scoring**: Score based on weighted document sections, sentence locations, and title for full text articles and abstracts as described in [Kafkas et al., 2017](https://doi.org/10.1186/s13326-017-0131-3). The aggregated scores of each gene/disease co-occurrence in the publication are further normalised between 0 and 1.

**Source**: [Europe PMC](http://europepmc.org)

**References**: [The Europe PMC Consortium, 2015](https://doi.org/10.1093/nar/gku1061); [Kafkas et al., 2017](https://doi.org/10.1186/s13326-017-0131-3)



### Expression Atlas

The EMBL-EBI Expression Atlas provides a differential expression pipeline aiming to identify genes that are differentially expressed in disease vs control samples. Only contrasts from studies with enough replicates and minimum quality criteria are included in the processing.

In a given contrast, to consider a gene significantly regulated in a contrast, all the following rules are required:

* Absolute log2 fold change > 1
* Adjusted p-value <= 0.05
* Maximum significant genes probes per contrast = 1000

In the Platform, each contrast from independent studies capturing differentially regulated genes constitutes independent evidence.

**Data type**: RNA expression

**Evidence scoring**: ExpressionAtlas scoring is the result of the product of:

* Scaled p-value from 0 (p = 1) to 1 (p<1e-10)
* Absolute log2 fold change divided by 10
* Percentile rank divided by 100

**Source**: [Expression Atlas](https://www.ebi.ac.uk/gxa/home)

**References**: [Papatheodorou, I. et al, 2020](https://doi.org/10.1093/nar/gkz947)



### **IMPC**

The genotype–phenotype associations made available by the International Mouse Phenotypes Consortium (IMPC) are used to identify models of human disease based on phenotypic similarity scores.

The Wellcome Sanger Institute PhenoDigm is an algorithm aimed at capturing the similarity between a knockout mouse and the clinical manifestations (phenotype) of a human disease. The premise is that if a gene knock-out causes an equivalent phenotype in mouse, the human counterpart is likely to be related with the cause of the disease.

It uses a semantic approach to map between clinical features observed in humans and mouse phenotype annotations. The phenotypic effects in mice are then mapped to phenotypes associated with human diseases. The matches are identified and a similarity score between a mouse model and a human disease is computed.

**Data type**: Animal model

**Evidence scoring**: The evidence score indicates the degree of concordance between the mouse and disease phenotypes, as described by [Smedley et al 2013](https://europepmc.org/abstract/MED/23660285).

**Direction of Effect assessment:**

<table data-full-width="false"><thead><tr><th>Direction on Target (Gain of Function (GoF) / Loss of Function (LoF))</th><th>Direction on Trait (Risk/Protective)</th></tr></thead><tbody><tr><td>Assumption of all variants LoF</td><td>Assumption of Risk</td></tr></tbody></table>

**Source**: [IMPC](https://www.mousephenotype.org)

**References**: [Smedley, D. et al, 2013](https://doi.org/10.1093/database/bat025)
