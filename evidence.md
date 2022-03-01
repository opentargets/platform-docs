# Target - disease evidence

## Target - disease evidence

Every event or set of events pinpointing a target as a potential causal gene or protein for a disease, represent the unit of information, most often referred as **evidence**. Within Open Targets, a series of pipelines ensure information is retrieved from their sources and standardised in a way that can be immediately applied to answer drug development queries.

All evidence is mapped to the reference target entity identifier (Ensembl gene) and disease or phenotype identifier (experimental factor ontology, EFO), as well as other reference controlled vocabularies and ontologies when appropriate. Evidence is also reviewed to minimise the presence of duplicates within the same data source.

Data sources are also grouped into bigger categories abstracting the type of evidence they predominantly capture. These categories are usually referred to in the platform as **data types** as opposed to the individual resource data referred to as **data sources**.

In order to contextualise the relative importance of each piece of evidence, the Open Targets Platform provides a scoring framework for each data source. This score will take more relevance when understanding the association scoring in later sections.

## Evidence data sources

### Open Targets Genetics Portal

Open Targets Genetics Portal focuses on the identification of trait-causal genes from significant loci in genome-wide association studies (GWAS).

Whereas GWAS identifies significantly-associated alleles (lead variants), these variants might not necessarily be the causal (or the only causal) ones. Moreover, the causal genes are not necessarily the closest to the lead variant. Due to these reasons, identifying target-disease associations based on GWAS data is extremely challenging. Open Targets Genetics tackles this and other challenges by applying cutting-edge statistical genetics methodologies into large-scale human genetics data. Moreover, Open Targets Genetics uses a machine learning method to identify the most likely causal genes by integrating and summarising the effect of tag variants based on genetic and functional genomic data. This method is referred as the [Locus2Gene model](https://genetics-docs.opentargets.org/our-approach/prioritising-causal-genes-at-gwas-loci-l2g).

A Genetics Portal evidence in the Platform is defined as any GWAS-significant lead variant (p-value < 1e-8) identified in a study with a predicted causal gene for the given trait with a Locus2gene score greater than 0.05.

**Datatype**: Genetic associations

**Evidence scoring**: [Locus2Gene (L2G) score](https://genetics-docs.opentargets.org/our-approach/prioritising-causal-genes-at-gwas-loci-l2g), filtered to use scores above 0.05

**Source**: [Open Targets Genetics Portal](https://genetics.opentargets.org)

**Reference**: [Ghoussaini M, et al. 2021](http://doi.org/10.1093/nar/gkaa840)

### PheWAS Catalog

The PheWAS Catalog provides a comprehensive analysis of significant phenome-wide associated loci. The list of phenotypes is derived from electronic medical records (EMR) represented in the DNA biobank BioVU produced by the Center for Precision Medicine at the Vanderbilt University Medical Centre. The EMR-based PheWAS uses ICD9 (International Classification of Disease, 9th edition), which were mapped to EFO using OLS and Zooma.

PheWAS Catalog evidence in the Platform is defined as any variant associated with a PheWAS-significant trait (uncorrected p-value < 0.05).

**Data type**: Genetic associations

**Evidence scoring**: Product of sample size scaled from 0 (n = 0) to 1 (n = 8,800) and scaled p-value from 0 (p = 0.5) to 1 (p = 1e-25)

**Source**: [PheWAS Catalog](https://phewascatalog.org)

**References**: [Denny, J. et al, 2013](https://doi.org/10.1038/nbt.2749)

### ClinVar

ClinVar is a NIH public archive of reports of the relationships among human variations and phenotypes, with supporting evidence. The ClinVar data source in the Open Targets Platform captures the subset of ClinVar that refers to germline variants (as opposed to somatic variants). Each evidence in the platform aims to capture an individual RCV record in ClinVar.

**Datatype**: Genetic associations

**Evidence scoring**: ClinVar evidence is scored in a 2-step process. In step 1, a score is assigned to every piece of evidence based on the clinical significance:

| Clinical significance                        | Evidence score |
| -------------------------------------------- | -------------- |
| association not found                        | 0              |
| benign                                       | 0              |
| not provided                                 | 0              |
| likely benign                                | 0              |
| conflicting data from submitters             | 0.3            |
| conflicting interpretations of pathogenicity | 0.3            |
| other                                        | 0.3            |
| uncertain significance                       | 0.3            |
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

**Source**: [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/) (via [European Variation Archive](https://www.ebi.ac.uk/eva/))

**References**: [Cook, C. et al, 2016](https://doi.org/10.1093/nar/gkv1352); [Landrum, M. et al, 2017](http://doi.org/10.1093/nar/gkx1153)

### Genomics England PanelApp

The Genomics England PanelApp is a knowledge base that combines crowdsourced expertise with curation to provide gene-disease relationships. Virtual gene panels related to human disorders are reviewed by experts within the clinical and scientific community to support the interpretation of genomes within the 100,000 Genomes Project. Within a panel, genes are rated based on the level of evidence supporting the association with the phenotypes identified by the panel. Genes are then classified according to a traffic light system with red/stop, amber/pause, and green/go classifications. To receive a green rating (diagnostic-grade) on a version 1+ panel, the gene requires "evidence from 3 or more unrelated families or from 2 - 3 unrelated families where there is strong additional functional data" and "genes that do not meet these criteria are rated as Amber (borderline) or Red (low level of evidence)."

The Open Targets Platform includes "green" and "amber" genes from version 1+ panels along with their phenotypes, providing the latter can be mapped to a disease or phenotype ontology. As we standardise our evidence to the EFO ontology, some of the phenotypes cannot be mapped and included in our platform - please visit the [Genomics England PanelApp website](https://panelapp.genomicsengland.co.uk) for the full set.

**Data type**: Genetic associations

**Evidence scoring**: Based on Genomics England gene rating:

| Gene Rating in GEL Panel | Evidence score |
| ------------------------ | -------------- |
| Amber                    | 0.5            |
| Green                    | 1              |

**Source**: [Genomics England PanelApp](https://panelapp.genomicsengland.co.uk)

**References**: [Martin, A. et al, 2019](https://doi.org/10.1038/s41588-019-0528-2)

### Gene2Phenotype

The data in Gene2Phenotype (G2P) is produced and curated from the literature by different sets of panels formed by consultant clinical geneticists. The G2P data is designed to facilitate the development, validation, curation, and distribution of large-scale, evidence-based datasets for use in diagnostic variant filtering. Each G2P entry associates an allelic requirement and a mutational consequence at a defined locus with a disease entity. A confidence level and evidence link are assigned to each entry. This confidence level follows the terminology described by [GenCC](https://thegencc.org/about.html) for describing gene-disease validity.

G2P evidence in the Platform is the result of any target-disease curation by any of the expert panels.

**Data type:** Genetic associations

**Evidence scoring:**

| **Gene2Phenotype confidence** | Evidence score |
| ----------------------------- | -------------- |
| Limited                       | 0.01           |
| Moderate                      | 0.5            |
| Strong                        | 1              |
| Both RD and IF                | 1              |
| Definitive                    | 1              |

**Source**: [Gene2Phenotype](https://www.ebi.ac.uk/gene2phenotype)

**References**: [Thormann, A. et al, 2019](https://doi.org/10.1038/s41467-019-10016-3)

### UniProt literature

The Universal Protein Resource (UniProt) provides a large-compendium of sequence and functional information at the protein level. As part of their functional annotation effort, UniProt curators also annotate proteins with publications supporting their involvement on pathogenic processes.

All publications supporting a given target disease relationship are aggregated into one single Platform evidence.

**Data type**: Genetic associations

**Evidence scoring**:&#x20;

| **Uniprot confidence** | Evidence score |
| ---------------------- | -------------- |
| Medium                 | 0.5            |
| High                   | 1              |

**Source**: [UniProt](https://www.uniprot.org)

**References**: [The UniProt Consortium, 2021](https://academic.oup.com/nar/article/49/D1/D480/6006196)

### UniProt variants

The Universal Protein Resource (Uniprot) also curate variants supported by publications that are known to alter protein function on disease. Curated mutations are predominantly protein coding or in regulatory regions clearly associated with the causal protein.

All publications supporting a given variant in connection with a disease constitute individual evidence. All supporting publications are aggregated within the same evidence.

**Data type**: Genetic associations

**Evidence scoring**:&#x20;

| **UniProt confidence** | Evidence score |
| ---------------------- | -------------- |
| Medium                 | 0.5            |
| High                   | 1              |

**Source**: [UniProt](https://www.uniprot.org)

**References**: [The UniProt Consortium, 2021](https://academic.oup.com/nar/article/49/D1/D480/6006196)

### ClinGen

The Clinical Genome Resource (ClinGen) Gene-Disease Validity Curation aims to evaluate the strength of evidence supporting or refuting a claim that variation in a particular gene causes a particular disease. ClinGen provides a framework of guidelines to assess clinical validity in a semi-quantitative manner allowing curators to classify the validity of given gene-disease pair.

All gene-disease pairs mapped to EFO constitute individual evidence in the Platform.

**Data type**: Genetic associations

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

### Orphanet

Orphanet is an international network that offers a range of resources to improve the understanding of rare disorders of genetic origin. These resources include an inventory of rare disease and gene associations, classification of the gene-disease relationship, information on the kind of mutation, and supporting publication references.

**Data type**: Genetic associations

**Evidence scoring:**

| Orphanet Disorder Gene Association Status | Evidence score |
| ----------------------------------------- | -------------- |
| Not yet assessed                          | 0.5            |
| Assessed                                  | 1              |

**Source**: [Orphanet Genes Associated with Rare Diseases](https://www.orpha.net/consor/cgi-bin/Disease\_Genes.php?lng=EN)

**References**: [Orphanet](https://www.orpha.net); [Orphadata](http://www.orphadata.org/cgi-bin/index.php)

### ChEMBL

The EMBL-EBI ChEMBL is a manually curated database of bioactive molecules with drug-like properties, either approved for marketing by the U.S Food and Drug Administration (FDA), or clinical candidates. ChEMBL also captures information regarding the drug molecule indications, as well as their curated pharmacological target.

In the Platform, ChEMBL evidence represents any target-disease relationship that can be explained by an approved or clinical candidate drug, targeting the gene product and indicated for the disease. Independent studies are treated as individual evidence.

**Data type**: Drugs

**Evidence scoring:** ChEMBL evidence is scored in a 2-step process. In step 1, a score is assigned to every piece of evidence based on the clinical precedence:

| Clinical Precedence | Evidence score |
| ------------------- | -------------- |
| Phase 0             | 0              |
| Phase I             | 0.1            |
| Phase II            | 0.2            |
| Phase III           | 0.7            |
| Phase IV            | 1              |

In Step 2, for those clinical trials that have stopped early, the score is down-weighted based on the classification of the reason to stop. In this way, less importance is attributed to evidence of studies that have been stopped due to negative outcomes or safety concerns:

| Reason to stop class   | Score weight |
| ---------------------- | ------------ |
| Negative               | 0,5          |
| Safety or side effects | 0,5          |

**Source**: [ChEMBL](https://www.ebi.ac.uk/chembl/)

**References**: [Mendez, D. et al, 2019](https://academic.oup.com/nar/article/47/D1/D930/5162468)

### Reactome

The Reactome database manually curates and identifies reaction pathways that are affected by a disease. Reactome annotation includes information regarding the causal target - disease link either being a protein coding mutation or an altered expression.

In the Platform, any mutation or altered expression event affecting a different reaction is captured in a different target - disease evidence.

**Data type**: Pathways & systems biology

**Evidence scoring**: All manually curated evidence in Reactome has a score of 1.

**Source**: [Reactome](https://reactome.org)

**References**: [Jassal, B. et al, 2020](http://doi.org/10.1093/nar/gkz1031)

### Project Score

Project Score is a Wellcome Sanger Institute resource that aims to combine gene fitness effects derived from CRISPR-Cas9 synthetic-lethality screenings, with tractability data and genomic biomarkers for a systematic prioritisation of targets. The resulting inferences are then mapped from the cancer cell lines in which the experiment is performed to their corresponding tumors.

In the Platform, any Project Score prioritised targets with scores greater than 41.5 are included as independent evidence.

**Data type**: Pathways & systems biology

**Evidence scoring**: Project Score priority score divided by 100.

**Source**: CRISPR (via[ Project Score](https://score.depmap.sanger.ac.uk))

**References**: [Behan, F. et al, 2019](https://doi.org/10.1038/s41586-019-1103-9)

### SLAPenrich

SLAPenrich (Sample-population Level Analysis of Pathway enrichments) is a novel statistical framework for the identification of significantly mutated pathways, at the sample population level, in large cohorts of cancer patients. SLAPenrich is based on a Poisson binomial model that takes into account the length of blocks of exons in genes within each pathway, and the background mutation rate of the analysed cohort of patients. SLAPenrich enrichment analysis is based on EMBL-EBI Reactome pathways and mutation data from The Cancer Genome Atlas ([TCGA](https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga)) cohort.

In the Platform, each pathway significantly enriched in tumor-occurring mutations constitute individual pieces of evidence.

**Data type**: Pathways & systems biology

**Evidence scoring**: Scaled enrichment p-value from 0.5 (p = 1e-4) to 1 (p<1e-14).

**Source**: [SLAPenrich](https://saezlab.github.io/SLAPenrich/)

**References**: [Iorio, F. et al, 2018](https://doi.org/10.1038/s41598-018-25076-6)

### Gene signatures



Data type: The platform also provides information about key driver genes for specific diseases that have been curated from Systems Biology analysis. These publications present different disease gene signatures as potential key drivers or key regulators causing disease.\*Pathways & systems biology

**Evidence scoring**: Scoring depends on whether the original data contains or not a score:

* p-values and rank-based scores are normalised to the 0.5 - 1 range
* If there is no score a fixed value of 0.5 is used

**References**: [Peters, L. A. et al, 2017](https://doi.org/10.1038/ng.3947); [Huan, T. et al, 2013](https://doi.org/10.1161/atvbaha.112.300112); [Zhang, B. et al, 2013](https://doi.org/10.1016/j.cell.2013.03.030); [Mostafavi, S. et al, 2018](https://doi.org/10.1038/s41593-018-0154-9)

### PROGENy

PROGENy (Pathway RespOnsive GENes) is a linear regression model that calculates pathway activity estimates based on consensus transcriptomic gene signatures obtained from perturbation experiments. PROGENy ([Schubert et al](https://www.nature.com/articles/s41467-017-02391-6.epdf?author\_access\_token=16QkzhJ3OA3qJDqBw\_GvGdRgN0jAjWel9jnR3ZoTv0NBFLUVI-ebH2AmtFlR1ykSPIho7ETJXL7VqZFC4zGtU0BaeoZncGrwx3ZW24lfVqvbSWqsQKaUXFTi\_c-4pgcpX-1qerWYlkG6sha8rhrnMg%3D%3D)) provides a framework to systematically compare pathway activities between normal and primary samples from The Cancer Genome Atlas (TCGA).

In the Platform, a PROGENy evidence is defined as any significantly regulated sample-level pathway activities inferred from matched normal vs. tumor samples.

**Data type**: Pathways & systems biology

**Evidence scoring**: Scaled p-value from 0.5 (p = 1e-4) to 1 (p<1e-14).

**Source**: [PROGENy](https://saezlab.github.io/progeny/)

**References**: [Schubert, M. et al, 2018](https://doi.org/10.1038/s41467-017-02391-6)

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

. All evidence has a base score of 0.5. Whereas tier 2 genes score is always 0.5, tier 1 scores can be modulated as follows:**References**: [Papatheodorou, I. et al, 2020](https://doi.org/10.1093/nar/gkz947)

### **Cancer Gene Census**

Cancer Gene Census (CGC) is part of the Wellcome Sanger Institute Catalogue of Somatic Mutations in Cancer ([COSMIC](http://cancer.sanger.ac.uk/cosmic)). CGC is an effort to catalogue genes which contain mutations that have been causally implicated in cancer. The exhaustive curation of the CGC covers individual studies as well as pan-cancer sequencing efforts, including The Cancer Genome Atlas (TCGA) and the International Cancer Genome Consortium (ICGC) among others.

In the Platform, CGC evidence is aggregated at the target - disease level to provide a summary of all curated evidence supporting the involvement of a target with a particular cancer type.

**Data type**: Somatic mutations

**Evidence scoring**: Scoring is based on [Cancer Gene Census tier sys](https://cancer.sanger.ac.uk/census)

| Modulator | Condition                                                                                         |
| --------- | ------------------------------------------------------------------------------------------------- |
| -0.25     | Only 1 mutated sample                                                                             |
| +0.25     | Gene mutated more frequently in particular disease compared to other diseases                     |
| +0.25     | Mutations in gene occur more frequently than in other genes of similar length in the same disease |

**Source**: [Cancer Gene Census](https://cancer.sanger.ac.uk/census)

**References**: [Sondka, Z. et al, 2018](https://doi.org/10.1038/s41568-018-0060-1)

### **IntOGen**

IntOGen provides a framework to identify potential cancer driver genes using large-scale mutational data from sequenced tumor samples. By harmonising tumor sequencing data from the ICGC/TCGA Pan-Cancer Analysis of Whole Genomes ([PCAWG](https://dcc.icgc.org/pcawg)) and other comprehensive efforts, IntOGen aims to provide a consensus assessment of cancer driver genes. Several state-of-the-art driver methodologies aiming to cover different approaches (e.g. dN/dS, Hotspots, etc.) are included to finally produce a consensus q-value for each driver gene in every tumor.

In the Platform, independent target - disease evidence are defined as any significant driver gene detected in any individual cohort. Information regarding the individual driver methods is also provided within each evidence.

**Data type**: Somatic mutations

**Evidence scoring**: Scaled [combined q-values](https://intogen.readthedocs.io/en/latest/drivers\_combination.html) from 0.25 (q = 0.1) to 1 (q < 1e-10).

**Source**: [intOGen](http://www.intogen.org/search)

**References**: [Martínez-Jiménez, F. et al, 2020](https://doi.org/10.1038/s41568-020-0290-x)

### **ClinVar (somatic)**

ClinVar is a NIH public archive of reports of the relationships among human variations and phenotypes, with supporting evidence. The ClinVar (somatic) data source in the Open Targets Platform captures the subset of ClinVar that refers to somatic variants (as opposed to germline variants).

Each evidence in the Platform aims to capture an individual RCV record in ClinVar.

**Datatype**: Somatic mutations

**Evidence scoring**: ClinVar evidence is scored in a 2-step process. In step 1, a score is assigned to every piece of evidence based on the clinical significance:

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

**Source**: [ClinVar](https://www.ncbi.nlm.nih.gov/clinvar/) (via [European Variation Archive](https://www.ebi.ac.uk/eva/))

**References**: [Cook, C. et al, 2016](https://doi.org/10.1093/nar/gkv1352); [Landrum, M. et al, 2017](http://doi.org/10.1093/nar/gkx1153)

### **Europe PMC**

The EMBL-EBI Europe PubMed Central (Europe PMC) enables access to a worldwide collection of life science publications and preprints from trusted sources. The Europe PMC data source aims to identify target - disease co-occurrences in the literature and provide an assessment on the confidence of the relationship. This pipeline uses deep-learning based Named Entity Recognition (NER) to identify gene/proteins and diseases when mentioned in the text, to later normalise them to the target or disease/phenotype entities in the Platform. All co-occurrences of both types of entities in the same sentence are considered evidence.

In the Platform, a piece of Europe PMC evidence is the result of aggregating all co-occurrences of the same target and disease within the same publication.

**Data type**: Text mining

**Evidence scoring**: Score based on weighted document sections, sentence locations, and title for full text articles and abstracts as described in [Kafkas et al., 2017](https://doi.org/10.1186/s13326-017-0131-3).

**Source**: [Europe PMC](http://europepmc.org)

**References**: [The Europe PMC Consortium, 2015](https://doi.org/10.1093/nar/gku1061); [Kafkas et al., 2017](https://doi.org/10.1186/s13326-017-0131-3)

### **PhenoDigm**

The Wellcome Sanger Institute PhenoDigm is an algorithm aimed to prioritise disease causing genes based on phenotype information. By leveraging the information from the International Mouse Phenotypes Consortium (IMPC) on mouse knock-out phenotypes, PhenoDigm aims to systematically map the phenotypes observed in mouse to potentially equivalent human diseases. The premise is that if a gene knock-out causes an equivalent phenotype in mouse, the human counterpart is likely to be related with the cause of the disease.

It uses a semantic approach to map between clinical features observed in humans and mouse phenotype annotations. The phenotypic effects in mice are then mapped to phenotypes associated with human diseases. The matches are identified and a similarity score between a mouse model and a human disease is computed. Details on the scoring are described elsewhere ([Smedley et al 2013](https://europepmc.org/abstract/MED/23660285)).

**Data type**: Animal models

**Evidence scoring**: Similarity score between a mouse model and a human disease described by [Smedley et al 2013](https://europepmc.org/abstract/MED/23660285).

**Source**: [PhenoDigm](https://www.sanger.ac.uk/tool/phenodigm/)

**References**: [Smedley, D. et al, 2013](https://doi.org/10.1093/database/bat025)

### Cancer Biomarkers

The Cancer Biomarkers database features biomarkers of drug sensitivity, resistance, and toxicity for drugs targeting specific targets in cancer, curated by clinical and scientific experts in precision oncology, and classified by cancer type.

One of the aims of the Cancer Genome Interpreter is to identify how variations in the tumour genome may influence its response to anti-cancer therapies. The Cancer Biomarkers database features biomarkers of drug sensitivity, resistance, and toxicity for drugs targeting specific targets in cancer, curated by clinical and scientific experts in precision oncology, and classified by cancer type.

**Data type:** Pathways & systems biology

**Evidence scoring:** All manually curated evidence in Cancer Biomarkers has a score of 1.

**Source:** [Cancer Genome Interpreter](https://www.cancergenomeinterpreter.org/biomarkers)

**References:** [Tamborero, D. et al, 2018](https://genomemedicine.biomedcentral.com/articles/10.1186/s13073-018-0531-8)

