---
description: Learn about the target prioritisation view
---

# Target Prioritisation

The new [target prioritisation page](https://platform.opentargets.org/disease/EFO_0005774/associations?table=prioritisations) can be accessed by clicking onto the **Target prioritisation factors** tab from the Associations on the Fly page when searching for targets associated with a disease or phenotype.

The view focuses on displaying target-specific properties in a disease agnostic way, which have been aggregated into four main sections—**Precedence, Tractability, Doability, Safety—**&#x61;nd individually scored by the Open Targets team.

A "traffic light" system has been designed to visually inform on target prioritisation, with the aim to facilitate target recommendations. Using a colour scale, green indicates potentially positive attributes and red indicates potentially negative attributes, providing information to help users assess the targets for further prioritisation or deprioritisation, respectively.



## Precedence section

### Target in clinic

**Definition:** Gene is targeted by available drugs in any clinical phase for any indication.

**Source of Data:** Platform Known Drugs widget ([ChEMBL](https://www.ebi.ac.uk/chembl/))

**Scoring:** Maximum clinical trial phase the target has been reported for, independently of the disease. Phases range from 0 to IV (corresponding to values of 0, 0.25, 0.5, 0.75 and 1 in the tool scores).



## Tractability section

### Membrane Protein

**Definition:** Target is annotated to be located in the cell membrane.

**Source of Data:** Platform Subcellular location widget \[HPA ([Human Protein Atlas](https://www.proteinatlas.org/)) and [UniProt](https://www.uniprot.org/)]

**Scoring:**

* 1 = Protein target is located (at least) in the cell or plasma membrane.&#x20;
* 0 = Protein target is not located in the cell membrane but some location information is accessible.&#x20;
* NA = No location information available.

### Secreted protein

**Definition:** Target is secreted or predicted to be secreted.

**Source of Data:** Platform Subcellular location widget \[HPA ([Human Protein Atlas](https://www.proteinatlas.org/)) and [UniProt](https://www.uniprot.org/)]

**Scoring:**

* 1 = Protein target is (at least) secreted or predicted to be secreted.&#x20;
* 0 = Not secreted but with location information.&#x20;
* NA = No location information available.

{% hint style="info" %}
Note: When contradictions between HPA (Human Protein Atlas) and UniProt exist (i.e. target is secreted according to HPA but in membrane according to UniProt), the information from HPA is taken.
{% endhint %}

### Ligand binder

**Definition:** Target binds at least one High-Quality Ligand according to ChEMBL tractability bucket.

**Source of Data:** Platform tractability widget ([Open Targets tractability](https://platform-docs.opentargets.org/target/tractability))

**Scoring:**

* 1 = Target has a high-quality ligand reported.&#x20;
* 0 = Target does not have high-quality ligand reported.
* NA = No information available.

### Small molecule binder

**Definition:** Target has been co-crystallised with a small molecule, reported in the Protein Data Bank.

**Source of Data:** Platform tractability widget ([Open Targets tractability](https://platform-docs.opentargets.org/target/tractability))

**Scoring:**

* 1 = Target has a small molecule reported.&#x20;
* 0 = Target does not have a small molecule reported.
* NA = No information available.

### Predicted pockets

**Definition:** Target has a [DrugEBIlity](https://chembl.blogspot.com/2010/10/drugebility-structure-based-component.html) score equal or above 0.7, which is predictive of harbouring a high-quality pocket.

**Source of Data:** Platform tractability widget ([Open Targets tractability](https://platform-docs.opentargets.org/target/tractability))

**Scoring:**

* 1 = Target contains a high-quality predicted pocket.&#x20;
* 0 = Target does not have a high-quality predicted pocket.
* NA= No information available.



## Doability section

> Models, tools and/or reagents that allow target assessment in preclinical settings to enable exploration of a given target

### Mouse ortholog identity

**Definition:** Mouse orthologs maximum identity percentage. A mouse harbouring an ortholog for the target of interest could be useful for _in vivo_ assaying.

**Source of Data:** Platform comparative genomics widget ([Ensembl Compara](https://www.ensembl.org/info/docs/api/compara/index.html))

**Scoring:**

From 0 to 1 are linearly scored those targets with at least one ortholog in mice harbouring at least 80% with the target.

* 1 = There is at least one gene in mice that contains a sequence with a 100% of identity with the target.
* 0 = There are no genes in mice containing a sequence with at least 80% of identity with the target.
* NA = No ortholog information.

{% hint style="info" %}
Note: Here we consider mouse orthologs and display the "query percentage identity" (percentage of the human target sequence that matches to the mouse gene) when there is an 80% identity or more. In the cases of targets with more than one ortholog, we take the one with the maximum query % ID.
{% endhint %}

### Chemical probes

**Definition:** Target has high quality chemical probes.&#x20;

> [Chemical probes](https://platform-docs.opentargets.org/target/chemical-probes-and-teps#chemical-probes) are small molecules acting as chemical modulators, binding reversibly to the target.

**Source of Data:** Platform Chemical probes widget ([Probes & Drugs](https://www.probes-drugs.org/home/))

**Scoring:**

* 1 = Target has high-quality chemical probes.
* 0 = Target does not have high-quality chemical probes.
* NA = No information available.



## Safety section

### Genetic constraint

**Definition:** Genes that are important for human physiology are seen to be depleted of deleterious variants. The Genome Aggregation Database ([gnomAD](https://gnomad.broadinstitute.org/)) has developed a continuous measurement of intolerance to loss of function (LoF) variants per gene, based on observed/expected LoF variant analysis. As recommended by gnomAD and implemented in the Open Targets platform, the rank of genes regarding their loss-of-function observed/expected upper bound fraction (LOEUF) metric is used ([LOEUF score](https://gnomad.broadinstitute.org/help/constraint#loeuf)).

**Source of Data:** Platform genetic constraint widget ([gnomAD](https://gnomad.broadinstitute.org/))

**Scoring:**

A score from -1 to 1 is given to genes depending on their LOEUF metric rank, being -1 the least tolerant to LoF variation and 1 the most tolerant.

### Mouse models

**Definition:** The international database Mouse Genome Informatics contains information about reported phenotypes when a gene is knocked-out in this animal model. These phenotypes are categorised in multiple phenotype classes, using an organ/system classification. We retrieve this information (available in our platform) and score the phenotypes classes regarding their severity (from 0 to -1). After aggregating all phenotypes with their scores according to the phenotype class they belong to, we use the harmonic sum to build a continuous score, which is normalised from 0 to -1.

**Source of Data:** Platform mouse phenotypes widget (Mouse Phenotypes, feeded from [MGI](https://www.informatics.jax.org/), a reference database for mice knockouts)

**Scoring:**

* Below 0 to -1 = When the target has been knocked-out in mice there were multiple and severe phenotypes reported, with a score higher than the first quartile.&#x20;
* 0 = Either the target has non-severe phenotypes reported or is in the first quartile of the normalised score.&#x20;
* NA = No information available.

{% hint style="info" %}
Note: Below you can find how we scored the mouse phenotype classes (-1 being the "most severe" and 0 "non relevant" phenotypes
{% endhint %}

<table><thead><tr><th>id</th><th width="395">Phenotype Class</th><th>score</th></tr></thead><tbody><tr><td>MP:0005370</td><td>liver/biliary system phenotype</td><td>-1</td></tr><tr><td>MP:0005385</td><td>cardiovascular system phenotype</td><td>-1</td></tr><tr><td>MP:0010768</td><td>mortality/aging</td><td>-1</td></tr><tr><td>MP:0003631</td><td>nervous system phenotype</td><td>-0.75</td></tr><tr><td>MP:0005388</td><td>respiratory system phenotype</td><td>-0.75</td></tr><tr><td>MP:0005367</td><td>renal/urinary system phenotype</td><td>-0.75</td></tr><tr><td>MP:0005376</td><td>homeostasis/metabolism phenotype</td><td>-0.75</td></tr><tr><td>MP:0005386</td><td>behavior/neurological phenotype</td><td>-0.75</td></tr><tr><td>MP:0005381</td><td>digestive/alimentary phenotype</td><td>-0.5</td></tr><tr><td>MP:0005379</td><td>endocrine/exocrine gland phenotype</td><td>-0.5</td></tr><tr><td>MP:0005382</td><td>craniofacial phenotype</td><td>-0.5</td></tr><tr><td>MP:0005377</td><td>hearing/vestibular/ear phenotype</td><td>-0.5</td></tr><tr><td>MP:0005384</td><td>cellular phenotype</td><td>-0.5</td></tr><tr><td>MP:0005380</td><td>embryo phenotype</td><td>-0.5</td></tr><tr><td>MP:0005394</td><td>taste/olfaction phenotype</td><td>-0.5</td></tr><tr><td>MP:0002006</td><td>neoplasm</td><td>-0.5</td></tr><tr><td>MP:0005375</td><td>adipose tissue phenotype</td><td>-0.5</td></tr><tr><td>MP:0005389</td><td>reproductive system phenotype</td><td>-0.5</td></tr><tr><td>MP:0005397</td><td>hematopoietic system phenotype</td><td>-0.5</td></tr><tr><td>MP:0005387</td><td>immune system phenotype</td><td>-0.5</td></tr><tr><td>MP:0005391</td><td>vision/eye phenotype</td><td>-0.5</td></tr><tr><td>MP:0005390</td><td>skeleton phenotype</td><td>-0.5</td></tr><tr><td>MP:0005369</td><td>muscle phenotype</td><td>-0.25</td></tr><tr><td>MP:0001186</td><td>pigmentation phenotype</td><td>-0.25</td></tr><tr><td>MP:0005378</td><td>growth/size/body region phenotype</td><td>-0.25</td></tr><tr><td>MP:0005371</td><td>limbs/digits/tail phenotype</td><td>-0.25</td></tr><tr><td>MP:0010771</td><td>integument phenotype</td><td>-0.25</td></tr><tr><td>MP:0002873</td><td>normal phenotype</td><td>0</td></tr></tbody></table>

### Gene essentiality

**Definition:** This target prioritisation feature flags common essential genes suggested by the aggregate analysis of a large number of cell lines across numerous cancer types. [DepMap](https://depmap.org/portal/) assigns common essential status to a gene by gene effect rank in the 90th percentile least dependent line. The emphasis is on the consistency rather than strength of the dependency.

**Source of Data:** Gene essentiality (`CRISPRInferredCommonEssentials.csv`) is sourced from the [DepMap Portal](https://depmap.org/portal/).&#x20;

**Scoring:**

* -1 = Target reported as essential
* 0 = Target not reported as essential
* NA = No information available

### **Known safety events**

**Definition:** Target is associated with curated adverse events.

**Source of Data:** Safety liability data from Platform safety widget ([Open Targets Safety](https://platform-docs.opentargets.org/target/safety)) and Open Targets downstream analysis of  toxicity datasets from [ClinPGx](https://www.clinpgx.org/).

**Scoring:**

* -1 = The target has at least one adverse event.
* NA = No information available.

### **Cancer driver gene**

**Definition:** Target is classified as an oncogene and/or tumour suppressor gene.

**Source of Data:** Platform Cancer Hallmarks widget ([COSMIC](https://cancer.sanger.ac.uk/census))

**Scoring:**

We use the attribute information from the cancer hallmarks, in the target profile. Here, targets considered as "cancer driver genes" are flagged as tumour suppressor, oncogene, or both

* -1 = Target is catalogued as driver gene (tumour suppressor, oncogene or both).
* NA = No information available.

### **Paralogues**

**Definition:** Paralogue maximum identity percentage.

**Source of Data:** Platform comparative genomics widget ([Ensembl Compara](https://www.ensembl.org/info/docs/api/compara/index.html))

**Scoring:**

* Below 0 to -1 are linearly scored those targets with at least one paralogue in human harbouring at least 60% of identity with the target.
* 0 = Those targets with paralogues harbouring less than 60% of identity.
* NA = No information available about paralogues for that target.

### Tissue specificity

**Definition:** HPA assessment on tissue-specific target expression.

**Source of Data:** Platform baseline expression widget ([ExpressionAtlas](https://www.ebi.ac.uk/gxa/home), [HPA](https://www.proteinatlas.org/) and [GTEx](https://www.gtexportal.org/home/)). We used the assessment for every target from the RNA expression data from the public version of Human Protein Atlas (proteinAtlasTissue)

**Scoring:**

<table><thead><tr><th width="579">Tissue specificity HPA assessment</th><th>Score</th></tr></thead><tbody><tr><td>Tissue enriched  >=4 fold higher mRNA in a given tissue compared to any other</td><td>1</td></tr><tr><td>Group enriched >=4 fold higher average mRNA in 2-5 tissue compared to any other</td><td>0.75</td></tr><tr><td>Tissue enhanced >=4 fold higher mRNA level in a given tissue compared to average of all other tissues</td><td>0.5</td></tr><tr><td>Low tissue specificity</td><td>-1</td></tr><tr><td>Not detected</td><td>NA</td></tr></tbody></table>

### Tissue **distribution**

**Definition:** HPA assessment on any detectable baseline expression for the target across tissues.

**Source of Data:** Platform baseline expression widget ([Expression Atlas](https://www.ebi.ac.uk/gxa/home), [HPA](https://www.proteinatlas.org/) and [GTEx](https://www.gtexportal.org/home/)). We used the assessment for every target from the RNA expression data from the public version of [Human Protein Atlas](https://www.proteinatlas.org/humanproteome/tissue).

**Scoring:**

<table><thead><tr><th width="580">Tissue distribution HPA assessment</th><th>Score</th></tr></thead><tbody><tr><td>Detected in single detected in a single tissue</td><td>1</td></tr><tr><td>Detected in some detected in more than one but less than 1/3 of tissues</td><td>0.5</td></tr><tr><td>Detected in many detected in at least 1/3 but not all tissues</td><td>0</td></tr><tr><td>Detected in all</td><td>-1</td></tr><tr><td>Not detected</td><td>NA</td></tr></tbody></table>

