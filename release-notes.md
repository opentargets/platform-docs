---
description: Summary of release highlights for the Open Targets Platform
---

# Release notes

## 26.09

#### **Release date**

25 September 2026

### Highlights

- **Major expansion of functional genomics (molecular QTL) data**, developed in collaboration
  with Kaur — **GTEx v10** plus two brand-new datasets, **IBDverse** and **MAGE** — added
  alongside the regular **GWAS Catalog** refresh. Together they add **~1.24M new credible
  sets** (3.52M → **4.76M**).
- **Two new gene-burden datasources** — **BRaVa** (multi-ancestry) and **Genes & Health**
  (British-Pakistani & Bangladeshi) — broadening rare-variant evidence and ancestry diversity.
- **Better handling of exome- and whole-genome-sequencing GWAS**, so large sequencing cohorts
  (e.g. UK Biobank, Genes & Health) now pass QC and contribute signal.
- **Updated genetic constraint** to **gnomAD v4.1.1** (now including chrX/chrY) plus a LOEUF
  binning fix.
- **Richer clinical-trial evidence** — trial sponsor on 100% of trials, dated approvals.
- **Cleaner disease associations** via cross-ontology de-duplication.
- **Pipeline, deployment and UI overhaul** — unified monorepo, ChEMBL feed on PostgreSQL,
  redesigned profile-page navigation, ArgoCD deployments.

### Data updates

**Functional genomics (molecular QTL).** New and upgraded molQTL data adds **~1.2M credible
sets** (molQTL total → 3.24M):

| Dataset                        | Credible sets | Δ vs 26.06 |
| ------------------------------ | ------------: | ---------: |
| **GTEx v10** (upgrade from v8) |     2,226,763 | +1,070,569 |
| **IBDverse** (new)             |        70,903 |    +70,903 |
| **MAGE** (new)                 |        56,793 |    +56,793 |
|                                |               |            |

- **IBDverse** ([#4469](https://github.com/opentargets/issues/issues/4469)) — an Open Targets project: a 2.2-million-cell single-cell atlas across 421
  individuals and >50 gut cell types ([Alegbe et al., *Nature* 2026](https://www.nature.com/articles/s41586-026-10627-z)),
  contributing **single-cell eQTLs** (42 cell types/contexts, 10,740 genes). It adds
  cell-type-resolved support to associations — e.g. **MAML2 × ulcerative colitis** in plasma
  cells and subepithelial intestinal fibroblasts.
- **MAGE** — eQTL/sQTL from 731 individuals across 26 populations / 5 continental groups
  ([Taylor et al., *Nature* 2024](https://www.nature.com/articles/s41586-024-07708-2)), adding
  ancestrally diverse expression data.

**GWAS Catalog refresh** ([#4424](https://github.com/opentargets/issues/issues/4424)). **+14,690 studies** (→ **163,181**) and **+44,859 credible sets**,
spanning **143 new publications**, with sync, curation, summary-statistics harmonisation and
fine-mapping (SuSiE + PICS). Highlighted new publications include a consensus **Alzheimer's
disease** meta-analysis and a multi-ancestry **endometriosis** GWAS.

**Better handling of exome/WGS studies** ([#4416](https://github.com/opentargets/issues/issues/4416)). QC thresholds tuned for array GWAS were failing
exome- and genome-sequencing studies; 26.09 relaxes them for ExWAS/WGS-flagged studies, so
large cohorts (e.g. UK Biobank, Genes & Health) now contribute signal. Studies carry new
analysis-type flags (`ExWAS`, `wgsGWAS`, `Metabolite`, `GxE`, `GxG`, non-additive,
multivariate) and QC flags, and study/credible-set pages now surface **SNP heritability**
(LDSC h², SE, intercept, mean χ², GC λ).

**New gene-burden evidence** ([#4468](https://github.com/opentargets/issues/issues/4468)). **10,611 new records** across 543 targets / 107 diseases:
- **BRaVa Consortium** — multi-ancestry: 9,098 records, 429 targets, 48 diseases.
- **Genes & Health** — British-Pakistani & Bangladeshi: 1,513 records, 184 targets, 73
  diseases.

**Genetic constraint (gnomAD v4.1.1)** ([#4494](https://github.com/opentargets/issues/issues/4494)). Canonical-transcript coverage 18,623 → 20,076, now
including **chrX/chrY** — well-known X-linked drug targets gain constraint for the first time
(e.g. **BTK**). A LOEUF binning bug was also fixed, shifting most genes' constraint bins.

**Clinical-trial evidence.** **Trial sponsor** ([#4442](https://github.com/opentargets/issues/issues/4442)) on 100% of trials; **approvals can now carry a
date** (partial subset, ~9%, from the clinical-report year); 220,810 clinical reports with
cleaner, reference-typed literature links.

**Cleaner disease associations** ([#4446](https://github.com/opentargets/issues/issues/4446)). Cross-ontology de-duplication merges **1,706 duplicate
disease terms** and consolidates **~3.16M evidence records** onto the correct term (e.g.
Obesity, Hypertension, Stroke).

### New product features

- **Genetic-quality display** ([#4417](https://github.com/opentargets/issues/issues/4417)) —
  study and credible-set pages now show harmonised summary-statistics QC and SNP-heritability
  metrics.
- **Redesigned profile-page navigation** — target, disease and drug profile pages have
  restructured navigation between sections and widgets.
- **Metrics page** ([#4328](https://github.com/opentargets/issues/issues/4328)) — a new single page showing headline release metrics (targets, diseases,
  drugs, studies, credible sets, evidence, variants, prioritised genes and colocalisations)
  plus a genetics breakdown by datasource.

### Pipeline updates

- **[Pipeline unification](https://github.com/opentargets/pipeline)** — the previously separate
  pipeline components were consolidated into a single monorepo.
- **ChEMBL feed migrated from Elasticsearch to PostgreSQL**
  ([#4485](https://github.com/opentargets/issues/issues/4485)) — makes ChEMBL-derived
  processing reproducible by third parties.
- **Target dataset refactor** ([#4457](https://github.com/opentargets/issues/issues/4457)) —
  the monolithic `target` object was split into standalone, by-`targetId` datasets (see schema
  changes).

### Technical improvements

- **Material UI upgrade** — the web app's component library was bumped for a more consistent,
  accessible interface.
- **ArgoCD deployments** — infrastructure moved to GitOps-style continuous deployment.
- **Storage encoding** — Arrow large types (`large_string`/`large_list`) and `zstd`
  compression across many datasets (20–45% smaller at equal row counts).

### Dataset & schema changes

Dataset- and field-level changes in the published data outputs (26.06 → 26.09). Diff key:
`+` added · `−` removed · `~` type/shape change. Row counts are from the 26.09 release.

**New datasets (from the target refactor).** `output/target` was split; these are now
standalone, by-`targetId` datasets:

| Dataset | Rows | Notes |
|---|--:|---|
| `output/transcript` | 644,292 | transcriptId, biotype, strand (int), exons[], TSS, uniprot/alphafold ids, isEnsemblCanonical |
| `output/homology` | 3,817,240 | species, homologyType, %identity, priority (from Compara) |
| `output/target_safety_event` | 4,387 | event, eventId, effects[], biosamples[], datasource, literature |
| `output/target_tractability` | 528,332 | modality, `category` (was `id`), value |
| `output/chemical_probe` | 1,265 | **renamed** from `chemical_probes` |
| `view/target_view` | 78,733 | backwards-compatible recomposition of the old nested `target` (for API/FE) |

`view/target_view` is a transitional compatibility shim (not a first-class distribution): it
deliberately **drops `tep` and `alternativeGenes`** and stubs three `transcripts[]`
sub-fields.

**Changed datasets:**
- `output/target` — slimmed; nested blocks (transcripts, tractability, safety, homologues,
  chemical probes) moved to the new datasets; **`tep` removed**
  ([#4470](https://github.com/opentargets/issues/issues/4470)).
- `output/target_essentiality` — `~ id → targetId`; `geneEssentiality` struct flattened
  (`isEssential`, `depMapEssentiality` at root).
- `output/target_prioritisation` — `− hasTEP`; LOEUF bins recomputed; constraint now
  gnomAD v4.1.1.
- `output/clinical_report` — `+ origin`, `+ provider`, `+ trialSponsor{agencyClass,name}`;
  `~ trialLiterature: list<string> → list<{id,type}>`
  ([#4489](https://github.com/opentargets/issues/issues/4489)); `− hasExpertReview`; `type`
  now means `INDICATION | SAFETY` (old `type` renamed to `origin`).
- `output/interaction` / `interaction_evidence` — `+ interactionId`; 10 A/B columns dropped
  ([#4474](https://github.com/opentargets/issues/issues/4474)).
- `output/chemical_probe` — `− probeMinerScore` (**breaking** for readers of this field).
- `output/drug_mechanism_of_action` — reshaped to one row per mechanism.
- `output/drug_warning` — `~ year: int64 → int32`.
- Strand encoding — `~ "+"/"-" → int 1/-1` (transcript / exons / canonicalTranscript)
  ([#4356](https://github.com/opentargets/issues/issues/4356)).

**Encoding-only changes** ([#4491](https://github.com/opentargets/issues/issues/4491))**.**
Broad `string → large_string` / `list → large_list` (Arrow large types) plus `zstd`
compression across many datasets — a 20–45% byte-size drop at flat row counts; not a logical
schema change.

### API changes (GraphQL)

Verified live on the release API (`apiVersion` 26.9.0 / `dataVersion` 26.09). POS and API
schema wiring for the release ([#4524](https://github.com/opentargets/issues/issues/4524)).

- **Target** — served via `view/target_view`, so the dataset split is **transparent to API
  consumers** (`transcripts`, `chemicalProbes`, `homologues`, `tractability`,
  `safetyLiabilities`, `canonicalTranscript` still resolve). **`tep` removed**;
  `canonicalTranscript.strand` is now a `Strand` enum.
- **Clinical reports** — `knownDrugs` replaced by **`drugAndClinicalCandidates`** → nested
  **`clinicalReports`** (`ClinicalReport`), with new `trialSponsor{name,agencyClass}`,
  `origin`, `source`, `provider`, and `trialLiterature{id,type}`; `type` = `INDICATION|SAFETY`;
  `hasExpertReview` removed.
- **Interactions** — identifier exposed as **`interactionIdentifier`** (string) on
  `InteractionEvidence` (the numeric join key is internal, not surfaced).
- **Target essentiality** — `isEssential` / `depMapEssentiality` resolve on `Target`.
- **Target prioritisation** — `hasTEP` removed.
- **New types** — `TrialSponsor`, `TrialLiterature`, `ClinicalReport`, `Strand`.
- **Fixes** — clinical reports returning `[]` everywhere (schema desync;
  [#4530](https://github.com/opentargets/issues/issues/4530)) and gene-burden evidence pages
  returning `count: 0` (null URL; [#4497](https://github.com/opentargets/issues/issues/4497))
  are both resolved.
- **Serving note** — four of the new target-satellite datasets (`chemical_probe`, `homology`,
  `target_safety_event`, `target_tractability`) are currently served only via `target_view`'s
  nested fields; standalone by-`targetId` access to them is deferred.

### Public data source versions

Versions configured for the 26.09 release. Rolling sources are fetched at their current
release.

| Source | Version |
|---|---|
| AACT (ClinicalTrials.gov) | 2026-08-25 |
| Cell Ontology | 2026-06-08 |
| ChEMBL | 37 |
| Clinical Mining | 2026-05-27 |
| COSMIC | 2025-06-24 (hallmarks 27-01-2026 v103) |
| DepMap | 2026Q1 |
| EFO | 3.93.0 |
| Ensembl | 116 |
| EVA / ClinVar | 2026-07-23 |
| Expression Atlas | 2025-07-14 |
| FinnGen | R12 |
| GENCODE | 50 |
| gnomAD | 4.1.1 |
| GTEx (baseline) | 11 |
| HPO | 2026-06-23 |
| IntOgen | 2024.06 |
| MONDO | 2026-08-04 |
| Open Targets Curation | 26.09.1 |
| Orphanet | current (product6) |
| Probes & Drugs | 01_2026 |
| Reactome | v95 (2026-01-19) |
| STRING | 12.0 |
| Uberon | 2026-06-23 |
| UniProt / HGNC / NCBI Gene / Gene Ontology | rolling (current release) |

### Overall data metrics

| Metric | 26.09 |
|---|--:|
| Targets | 78,733 |
| Diseases and phenotypes | 45,896 |
| Drugs and compounds | 19,170 |
| Evidence strings | 41,977,200 |
| Target-disease associations | 17,459,960 |
| Variants | 7,886,762 |

More detailed and interactive metrics — including studies, credible sets, prioritised genes
and colocalisations, with a genetics breakdown by datasource — can now be explored live on the
Platform **metrics page**.

## 26.06

#### **Release date**

24 June 2026

### Highlights

#### Data updates

Data updates in this release include:

* New ChEMBL 37
* New PanelApp NHSE Genomic Medicine Service panel
* Latest IMPC data
* Latest GWAS Catalog studies

The GWAS Catalog update adds over 14,000 studies from 111 publications, including 27,689 credible sets and more than 105,000 variants.

* Alignment to EFO 3.88

EFO 3.88 replaces many disease identifiers with Mondo identifiers. The Platform has been updated to reflect these ontology changes.

#### New product features

**New baseline expression**&#x20;

We have completely revamped and expanded our baseline expression dataset with:

* Single-cell RNA sequencing data from [Tabula Sapiens](https://tabula-sapiens.sf.czbiohub.org/)
* Bulk RNA sequencing data from [Genotype-Tissue Expression (GTEx)](https://gtexportal.org/home/) and the [Database of Immune Cells (DICE)](https://dice-database.org/)
* Mass spectrometry proteomics datasets from the [PRoteomics IDEntifications Database (PRIDE)](https://www.ebi.ac.uk/pride/), which was set up as part of an Open Targets project.
* New visualisations

Users can now explore the new baseline expression data through a [redesigned widget](https://staging.platform.opentargets.org/target/ENSG00000133703), at both tissue and cell type level.

**Target prioritisation using baseline expression data**

* The target prioritisation view has also been updated with new expression distribution and specificity scores for tissues and cell types. Please refer to the dedicated [documentation page](https://platform-docs.opentargets.org/web-interface/target-prioritisation) for more info on the target prioritisation assessment method.

**Subcellular location widget**

* The subcellular location widget now displays isoform-specific localisation information from UniProt sources.

**New Drug molecule representations**

* Drug pages now use updated molecular structure images from ChEMBL.

#### Pipeline updates

**Clinical Mining**

* We have improved extraction of drug-disease relationships from AACT clinical trial data using LLM-based methods, increasing accuracy and reducing false-positive association.
* This update has added 4,742 additional clinical reports from AACT, 32,518 drug indication pairs, and 292,325 clinical precedence evidence.

**Locus-to-Gene**

* Two new trans-pQTL features (_transPQtlColocH4Maximum_ and  _transPQtlColocH4MaximumNeighbourhood_) have been incorporated into the L2G pipeline, improving causal gene prioritisation by leveraging molecular interaction data.

**Literature**

* Updates to the literature pipeline, including improved ontology mapping, entity disambiguation, and co-occurrence generation, have increased evidence coverage while reducing false positive associations.&#x20;
* Overall, these changes add approximately 1.8 million evidence records and remove around 600,000 direct associations.

#### Technical improvements

**New search now supporting:**

* Clinical trial NCT identifiers
* Additional variant query formats
* Disease/ontology identifiers using either colon or underscore notation

**Associations page URL synchronisation**

* URLs now preserve page state, including filters, scoring settings, pinned targets and open widgets

**Infrastructure changes**&#x20;

* Started creation of a public Helm Chart for deploying a whole Platform in Kubernetes
* New revision mechanics to support data versioning and release management
* Migration of POS to Otter 26
* Created a knowledge base with technical docs on operations, release process
* New POS workflow step for loading data into AWS

### More info and overall metrics

* 78,691 targets
* 47,080 diseases and phenotypes
* 22,407 drugs and compounds
* 42,394,639 evidence strings
* 17,199,165 target-disease associations
* 7,538,243 variants

Check out the 26.06 release [blog post](https://blog.opentargets.org/open-targets-platform-26-06-has-been-released/) for more information on the new features and datasets introduced in this release.

Visit the Open Targets Community [26.06 release post](https://community.opentargets.org/t/26-06-release-now-live/2045) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 26.03

#### Release date

23 March 2026

### Highlights

#### Data updates

* The latest GWAS Catalog data adds 710 new studies from 97 publications, resulting in over 5,000 new credible sets
* This update includes 780 credible sets from the biggest study for hypothyroidism ever ingested in the Platform:  ([Rand SA et al. Nat Genet, 2025](https://www.nature.com/articles/s41588-025-02410-z))
* New data from ClinVar and ClinPGx through the European Variation Archive, as well as updates from String DB and IntAct

#### New product features

* Designed and implemented a new [clinical mining pipeline](https://github.com/opentargets/clinical_mining), which expands the data sources for clinical information,  integrating and annotating data from:
* [ClinicalTrials.gov](http://clinicaltrials.gov) via AACT,
* ChEMBL curated indications,&#x20;
* ChEMBL drug warnings,
* Therapeutic Target Database (TTD),
* European Medical Agency Human Medicines (EMA),&#x20;
* Japan’s Pharmaceuticals and Medical Devices Agency Approvals (PMDA)

The outputs of the new pipeline are presented to users through our re-designed clinical-centric widgets: Indications (Drug pages), Drugs and Clinical Candidates (Target and Disease and Target Prioritisation pages) and Clinical Precedence (new evidence feed in the Associations page)

See the new [clinical reports section](https://platform-docs.opentargets.org/drug/clinical-report) in Platform documentation for more details.

* Added enhancer-gene regulatory predictions from the [ENCODE Project rE2G model](https://www.biorxiv.org/content/10.1101/2023.11.09.563812v1) to the Locus-to-Gene (L2G) framework, introducing new features (`e2gMean` and `e2gNeighbourhoodMean`) that incorporate probabilistic regulatory interactions to improve gene prioritisation
* Enhanced association data with \~98% date coverage to improve novelty estimation, and integrated novelty/time-series calculations directly into the association pipeline by introducing a unified schema with an embedded `timeseries` field (capturing yearly scores, evidence and novelty) to support upcoming novelty features. The association dataset schema has been revised to better reflect this integration - please take a look at our [download page](https://platform.opentargets.org/downloads) for details&#x20;
* Resolved disease–phenotype duplications in the ontology by merging evidence for overlapping terms, removing \~300 duplicates and improving data consistency across the Platform
* Updated LD annotation by correcting the liftover process, fixing coordinate errors that affected finemapping in <1% of credible sets

#### Data access

* **AWS:** Open Targets Platform data is now available on Amazon Web Services (AWS) through the Open Data Program. You can find more information on how to access the Open Targets AWS buckets [here](https://platform-docs.opentargets.org/data-access/platform-datasets-on-aws) or through the 'access data' tabs from our [download page](https://platform.opentargets.org/downloads)
* **Open Targets MCP:** We have released an update to the MCP, with improved biological domain awareness, reducing token usage and enhancing query efficiency

#### Technical  enhancements&#x20;

* Implemented first version of End-to-End testing to improve the stability of the Platform. See [here](https://github.com/opentargets/ot-ui-apps/tree/main/packages/platform-test#readme) for more details
* Migrated all non-search datasets from OpenSearch to ClickHouse, resulting in a \~2× improvement in API query performance
* Resolved minor scoring inconsistencies between the API and web interface by aligning default settings
* Variant page viewer component refactored for reusability
* Fixed a number of FE bugs

Check out the [26.03 release **blog post**](https://blog.opentargets.org/open-targets-platform-26-03-has-been-released) for more information on the new features and datasets introduced in this release.

#### Overall data metrics

* 78,691 targets
* 47,030 diseases and phenotypes
* 22,230 drugs and compounds
* 34,086,838 evidence strings
* 12,466,856 target-disease associations
* 7,432,549 variants

Visit the [**Open Targets Community 26.03** **release thread**](https://community.opentargets.org/t/26-03-release-now-live/1987) for more data metrics for this release, including a per datasource breakdown of evidence strings

## 25.12

### Release date

10th December 2025

### Highlights

#### Data updates

* The latest GWAS Catalog data adds an impressive 78% additional credible sets, most of which are from:

1. UK Biobank Whole-Genome Sequencing Consortium’s [study of 490,640 UK Biobank participants](https://www.nature.com/articles/s41586-025-09272-9)&#x20;
2. Karczewski, Gupta, and Kanai’s [Pan-UK Biobank genome-wide association analyses](https://www.nature.com/articles/s41588-025-02335-7)
3. Zoodsma M, et al. [UK Biobank human metabolite meta analysis](https://www.nature.com/articles/s41588-025-02355-3)

* New update from [CHEMBL 36](https://chembl.blogspot.com/2025/09/chembl-36-is-out.html), including new  molecules, indications and drug warnings
* New data from [Ensembl 115](https://www.ensembl.info/2025/09/02/ensembl-115-has-been-released/), Probes\&Drugs, Reactome, and EVA (through ClinVar)

#### New product features

* New COLOC-PIP colocalisation methodology in Gentropy for the colocalisation of overlapping GWAS-GWAS and GWAS-molQTL credible sets. This method was adapted from [Giambartolomei et al. , 2014](https://journals.plos.org/plosgenetics/article?id=10.1371/journal.pgen.1004383)
* Removed all SuSiE fine-mapping credible sets for multi-ancestry GWAS
* Our credible set pages now have a new widget showcasing Enhancer-to-Gene (E2G) predictions from the ENCODE-rE2G model ([Gschwind\*, Mualim\*, Karbalayghareh\*, Sheth\*, Dey\*, Jagoda\*, Nurtdinov\*, and Xi\* et al., bioRxiv](https://www.biorxiv.org/content/10.1101/2023.11.09.563812v1)). Please note that we have also renamed the widget “Enhancer-to-Gene” rather than “Intervals”
* Measurement traits are now filtered out by default from the target association view, with an option to include them back if needed. This new functionality aims to highlight direct links between target and diseases
* Three sources of target-disease evidence were removed from our associations view -  PROGENy, SLAPenrich, and Gene Signatures (SysBio) - as their data has been superseded by the information contained in other sources
* [Download files](https://platform.opentargets.org/downloads) are now split by data sources, with the aim to facilitate investigation of individual evidence
* Our GraphQL API schema documentation was expanded&#x20;

#### Technical  enhancements&#x20;

* Large-scale refactoring of the [orchestration](https://github.com/opentargets/orchestration) of Open Targets Platform pipelines
* Following up from a rewrite in [OnToma](https://github.com/opentargets/OnToma), our Python package for ontology mapping, we have enhanced mapping of disease phenotypes for several evidence sources such as ClinGen, Gene2Phenotype, Orphanet, Genomics England PanelApp, IMPC, Gene Burden, and Pharmacogenetics

Check out the [25.12 release blog post](https://blog.opentargets.org/open-targets-platform-25-12-has-been-released/) for more information on the new features and datasets introduced in this release.

#### Key metrics

| Metric                    | Count      |
| ------------------------- | ---------- |
| Targets                   | 78,725     |
| Diseases/phenotypes       | 46,960     |
| Drugs/clinical candidates | 18,475     |
| Evidence                  | 32,515,132 |
| Associations              | 12,010,760 |

Visit the [Open Targets Community 25.12 release thread](https://community.opentargets.org/t/25-12-release-now-live/1951) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 25.09

### Release date

17 September 2025

### Highlights

* New intervals datasets on variant page: includes over 13 million enhancer-gene regulatory interactions across 352 cell types and tissues from [Gschwind et al.’s](https://www.biorxiv.org/content/10.1101/2023.11.09.563812v1) ENCODE-rE2G model
* Added full list of 95% molQTL credible sets on target page&#x20;
* New version of variant page structural viewer (from new FE component) - now including additional options for users to navigate structure confidence, pathogenicity, domains, secondary structure, residue hydrophobicity&#x20;

### Data updates

* New GWAS Catalog update (+30,000 new credible sets)
* Expression Atlas:  new differential expression dataset, adding around 6,000 new unique target-disease associations to the Platform
* Gene-level synonymous, missense, and loss-of-function constraint scores have been updated from gnomAD v2 to v4
* Updated DepMap data (25Q2) used for the essentiality widget, introducing survival results for 17876 genes for 5 new cell lines
* Added 67 new chemical probes following up from the latest Probes\&Drugs release

### Product enhancements and bug fixes

* 99% of evidence now has date (evidenceDate), with 100% coverage for GWAS credible set derived evidence. This is part of a [recently preprinted](https://www.researchsquare.com/article/rs-5669559/v1) Open Targets project to help assess novelty of disease target associations
* Deployment on new Kubernetes-based cluster infrastructure
* Streamlined L2G pipeline&#x20;
* PharmGKB, a source of pharmacogenetics data, has been rebranded to ClinPGx. This change is now reflected in the Platform
* Bug fixes and improvements spanning across data, back-end and front-end

Check out the [25.09 release blog](https://blog.opentargets.org/open-targets-platform-25-09-release/) post for more information on the new features and datasets introduced in this release

### Overall data metrics

* 78,726 targets
* 39,530 diseases and phenotypes
* 18,119 drugs and compounds
* 30,396,274 evidence strings
* 10,989,518 target-disease associations

Visit the [Open Targets Community 25.09 release thread](https://community.opentargets.org/t/25-09-platform-release-now-live/1929) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 25.06

### Release date

18 June 2025

### Highlights

**New features**

* A new Target Interactors view, which allows you to view association evidence target interactors directly in the disease associations page. Users can choose one of four sources of molecular interactors and view the association evidence for the top scoring interactors for that database.
* A revamped data downloads page, making Open Targets Platform data more FAIR. The data follows the [Croissant](https://mlcommons.org/working-groups/data/croissant/) metadata standard format, based on JSON-LD, developed by ML-Commons.

**Data updates**

* The latest GWAS Catalog data adds 36% more credible sets, most of which are from the [VA Million Veteran Program](https://www.research.va.gov/mvp/) study.
* Burden evidence from the [Broad CVDI Human Disease Portal](https://hugeamp.org:8000/research.html?pageid=600_traits_app_home).
* Experimental Factor Ontology (EFO) replaced measurement terms with terms from the Ontology of Biological Attributes (OBA), and is now reflected in the Platform.
* New data from Reactome, Europe PMC, COSMIC and EVA (through ClinVar).

**Product features**

* Updated version of the Molecular Structure viewer on target profile pages. We also added a new version of the viewer on missense variant pages, which indicates the location of the variant in the AlphaFold model and view AlphaMissense pathogenicity scores.
* Pharmacogenetics widgets on the variant, target, and drug profile pages now have an additional Directionality column.

**Product enhancements and bug fixes**

* Strengthened our search functionality with performance optimisations and additional filtering capabilities.
* Case-case studies have been removed from our GWAS data as these are difficult to map to the correct disease.
* Method descriptions to variant effect widget and bug fixes on variant page.

Check out the [25.06 release blog post](https://blog.opentargets.org/open-targets-platform-25-06-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 78,726 targets
* 38,959 diseases and phenotypes
* 18,081 drugs and compounds
* 29,602,753 evidence strings
* 10,563,905 target-disease associations

Visit the [Open Targets Community 25.06 release thread](https://community.opentargets.org/t/25-06-platform-release-now-live/1828/1) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 25.03

### Release date

19 March 2025

### Highlights

**New features**

* Variant, study, and credible set information is now available in the Open Targets Platform. This unites the Open Targets Platform and Open Targets Genetics into a single interface for human genetic and target discovery information.
* Interpret gene-disease evidence from both common and rare variation in one resource, and in multiple ancestries.
* The Platform now has three additional entities:
  * [Variant](variant.md): functional context for 6.5M rare and common variants
    * Please note: the Platform only integrates variants associated with a disease, trait, or phenotype
  * [Study](study.md): GWAS and molQTL studies
  * [Credible Set](credible-set.md): 2.6 million credible sets derived from various sources
    * Colocalisation is now based on credible set overlaps
* A new [Locus-to-Gene (L2G)](gentropy/locus-to-gene-l2g.md) machine learning model which prioritises likely causal genes at each GWAS locus by using functional genomics features. The Platform also uses [Shapley values](credible-set.md#explaining-l2g-predictions) as part of the L2G predictions to illustrate the relative contribution of each feature.

**Data updates**

* A substantial increase in the literature evidences due to improvements in resolving disambiguation of entities.
* Updated gene burden data through FinnGen R12.
* New NHS Genomic Medicine Service panels from GEL PanelApp and a new hearing loss panel to the Gene2Phenotype evidence set.
* Rewritten Uniprot pipeline with new associations from Uniprot variants
* Updated data from Probes\&Drugs and DepMap.
* New data from Reactome, ChEMBL, Europe PMC, COSMIC and EVA (through ClinVar).

**Product features**

* A new Scalable and reproducible genetic analyses pipeline available as a Python package for post-GWAS analysis: [Gentropy](https://opentargets.github.io/gentropy/).
* An updated data downloads page which has a more detailed description of each file. (Temporary removal of schema which will be brought back in the subsequent release).
* [otter](https://github.com/opentargets/otter) - **O**pen **T**argets' **T**ask **E**xecuto**R** i.e. scripts that process and prepare data for our ETL pipelines.
* Various improvements to our web interface:
  * Users can search the UI using variants and study id.
  * Improved searching, filtering and sorting of entities on our associations pages. In particular, there are now separate sections for uploaded entity lists and pinned entities, and you can remove individual filters from the view.
  * The platform and the Target Prioritisation view has a more accessible colour scheme.\
    Option to select desired columns in the UI.
  * A graphical Comparative Genomics view in Target Prioritisation.
  * Preview on hover: Ability to view details of an entity without navigating to it.

**Product enhancements and bug fixes**

* Filtered out Phase IV clinical trial evidence that lacks regulatory approval for the specific indication from our target-disease association data.
* The BE infrastructure has been upgraded to Scala 3
* Improved and restructured documentation.

{% hint style="info" %}
Post 25.03, the data downloads paths have changed as now only parquet file format is available. Also there are minor changes to the name of the dataset (snake\_case & singular). More details can be found [here](https://community.opentargets.org/t/issues-with-gcp-big-query/1704/5).

* Previous releases (till 24.09):
  * `https://ftp.ebi.ac.uk/pub/databases/opentargets/platform/24.09/output/etl/parquet/associationByOverallDirect/`
* 25.03 release (and therafter):&#x20;
  * `https://ftp.ebi.ac.uk/pub/databases/opentargets/platform/25.03/output/association_by_datasource_direct/`
{% endhint %}

Check out the [25.03 release blog post](https://blog.opentargets.org/open-targets-platform-25-03-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 78,766 targets
* 28,513 diseases and phenotypes
* 18,081 drugs and compounds
* 28,168,992 evidence strings
* 10,162,821 target-disease associations
* 6,493,882 variants

Visit the [Open Targets Community 25.03 release thread](https://community.opentargets.org/t/25-03-platform-release-now-live-open-targets-genetics-data-update/1708) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 24.09

### Release date

18 September 2024

### Highlights

**New features**

* Users now have the ability to apply target-specific or disease/phenotype-specific filters to the target-disease association and target prioritisation pages. Read more details about the feature in our [documentation](https://platform-docs.opentargets.org/web-interface/associations-on-the-fly#filtering-functionality).

**Data updates**

* New safety liabilities associated with several targets which are routinely used by pharmaceutical companies have been added, from Brennan et al. (2024).
* New Gene Burden evidence from the LoF burden analyses in FinnGen’s latest public release (R11).
* New data from Reactome, Europe PMC, COSMIC and EVA (through ClinVar).

**Product features**

* Improved visualisation for Gene essentiality data from Cancer DepMap.
* Updated frontend table design and functionality leading to better searching/filtering and sorting functionality for most tables in the UI.
* The classic associations view has been deprecated from the Platform..

**Product enhancements and bug fixes**

* OpenAI model in the literature summarisation tool was updated to GPT-4o-mini.
* Changes to `variant` field in the cancer biomarker evidence.
* Aggregated the granularity of the description of phenotypes inside `cohortPhenotypes` to resolve duplication in ChEMBL evidence.
* Bug fixes: pharmacogenetics schema, molecule dataset.

Check out the [24.09 release blog post](https://blog.opentargets.org/open-targets-platform-24-09-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 63,121 targets
* 28,327 diseases and phenotypes
* 18,041 drugs and compounds
* 17,853,184 evidence strings
* 8,155,988 target-disease associations

Visit the [Open Targets Community 24.09 release thread](https://community.opentargets.org/t/24-09-platform-release-now-live/1556) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 24.06

### Release date

19 June 2024

### Highlights

**New features**

* Uploading a custom list of targets or diseases to obtain a tailored associations view allowing users to view selected target-disease evidence for the specific entities.

**Data updates**

* Integration of ChEMBL 34 which now contains data from the European Medicines Agency (EMA) increasing drug-indication coverage.
* Updates to the clinical trials and tractability data.
* Updating the gene burden results from AstraZeneca’s PheWAS portal [version 5](https://azphewas.com/about).
* New gene burden evidence for schizophrenia from the SCHEMA consortium and ancestry-specific evidence for prostate cancer.
* A new Gene2Phenotype panel with musculo-skeletal implications.
* New data from Reactome, COSMIC and EVA (through ClinVar), Probes and Drugs and GEL PanelApp increasing our coverage of data.

**Product features**

* Ability to handle pharmacogenetic evidence involving drug combinations.

**Product enhancements and bug fixes**

* Exclusion of splice QTLs from the assessment for the direction of effect and selecting the beta from the evidence with the lowest p-value instead of the largest effect size.
* Improvements in the AotF GQL Playground Component.
* Dropping `isHumanApplicable` field from target safety.
* Bug fixes to the ClinVar (somatic) widget loading state.
* Resolving an error in phenotype mapping in GEL PanelApp, resolving incorrect tractability precedence and removing categorical burden tests from Genebass data based on community feedback.

Check out the [24.06 release blog post](https://blog.opentargets.org/open-targets-platform-24-06-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 63,226 targets
* 28,198 diseases and phenotypes
* 18,041 drugs and compounds
* 17,703,456 evidence strings
* 8,079,215 target-disease associations

Visit the [Open Targets Community 24.06 release thread](https://community.opentargets.org/t/24-06-platform-release-now-live/1455) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 24.03

### Release date

20 March 2024

### Highlights

**New features**

* Implementation of direction of effect assessment for eight different sources of target-disease association evidence.
* Filtering bibliography data based on a publication date.

**Data updates**

* Integration of the latest dataset from Project Score.
* Integration of the 23Q4 version of DepMap ([depmap.org](https://depmap.org)).
* New data from Reactome, COSMIC and EVA (through ClinVar) increasing our coverage of data.

**Product features**

* Inclusion of star alleles from PharmGKB and a new _Direct Drug Target_ column to the pharmacogenetics widget.
* Use of pharmacogenetics data to inform adverse drug response as an additional source of information on target safety.
* New dedicated GraphQL API query playground for Associations-on-the-Fly and target prioritisation view.

**Product enhancements and bug fixes**

* Redesigned context menu with a new navigation and pinning behaviour.
* Updated protvista-uniprot viewer library to v2.11.1.
* Bug fixes to download file schema and search issues.

Check out the [24.03 release blog post](https://blog.opentargets.org/open-targets-platform-24-03-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 63,226 targets
* 25,817 diseases and phenotypes
* 17,111 drugs and compounds
* 17,317,290 evidence strings
* 7,802,260 target-disease associations

Visit the [Open Targets Community 24.03 release thread](https://community.opentargets.org/t/24-03-platform-release-now-live/1374) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 23.12

### Release date

30 November 2023

### Highlights

**New features**

* 'Target Prioritisation' view: A new view for assessment of the target features considered when prioritising (or deprioritising) targets for drug discovery. Watch a detailed video [here](https://www.youtube.com/watch?v=WQwQn6I4jkw).
* A new widget in the Platform adding pharmacogenetics data from PharmGKB.

**Data updates**

* New data available on Baseline RNA and protein expression data for targets via the API and FTP.
* New data from Reactome and EVA (through ClinVar) increasing our coverage of data.

**Product features**

* Users can easily export the entire associations table and the target prioritisation table in json or tsv format.
* Updated search bar design with search suggestions.

**Product enhancements and bug fixes**

* Transition to OpenSearch from Elasticsearch.
* Bug fixes in the widgets in the Association On The Fly view and styling issues.

Check out the [23.12 release blog post](https://blog.opentargets.org/open-targets-platform-23-12-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 62,733 targets
* 25,246 diseases and phenotypes
* 17,095 drugs and compounds
* 16,710,896 evidence strings
* 7,994,180 target-disease associations

Visit the [Open Targets Community 23.12 release thread](https://community.opentargets.org/t/23-12-platform-release-now-live/1294) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 23.09

### Release date

21 September 2023

### Highlights

**New features**

* ‘Associations on the Fly’ - revamp of the current Open Targets Platform association page with new facets and additional built-in functionalities like view data directly in the associations table, control weights of contributing evidence, filter by datasource and data type (OR filters) and pin rows. Watch a detailed video [here](https://www.youtube.com/watch?v=2A9bksboAag).
* OpenAI Literature Summarisation tool - For data features that link to publications, users can ask for a natural language summary of the target-disease evidence presented in the publication using LangChain and OpenAI’s GPT3.5 Turbo model.

**Data updates**

* Updated Molecular Interactions data source [STRING Database](https://string-db.org/) to version 12.0
* Increase in Europe PMC literature evidence by 9.9% to 10,355,423
* New data from ChEMBL, COSMIC and EVA (through ClinVar) increasing our coverage of data

**Product features**

* Easy access to the schema of the files available for download in the Open Targets Platform

**Product enhancements and bug fixes**

* Expanded the definition of a drug to include all probes as reported by [Probes & Drugs Portal (P\&D)](https://www.probes-drugs.org/home/) as chemical probes are useful from a target's doability perspective
* Open Targets Platform user interface migration to Material UI v5
* Refactoring of the sections in the frontend codebase - Components and sections moved into the packages/sections and packages/ui

Check out the [23.09 release blog post](https://blog.opentargets.org/open-targets-platform-23-09-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 62,733 targets
* 25,209 diseases and phenotypes
* 17,096 drugs and compounds
* 16,232,046 evidence strings
* 7,922,844 target-disease associations

Visit the [Open Targets Community 23.09 release thread](https://community.opentargets.org/t/the-latest-release-22-09-is-now-live/1212) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 23.06

### Release date

26 June 2023

### Highlights

**New features**

* Addition of a CRISPR Screens widget featuring data from [CRISPRBrain](https://crisprbrain.org/)
* Introduction of a Cancer DepMap widget showcasing gene essentiality data from the [Cancer DepMap Portal](https://depmap.org/portal/)

**Data updates**

* Updated data from ChEMBL, including adverse event drug warning data and more granular information on clinical phases
* New data from IntoGEN, Europe PMC, and EVA (through ClinVar) increasing our coverage of data

**Product features**

* Missense variants in the OT Genetics, UniProt variants and ClinVar widgets now link to [ProtVar](https://www.ebi.ac.uk/ProtVar/), a new tool to interpret the functional consequences of human missense variants

**Product enhancements and bug fixes**

* Fixes - homology widget, fixes to the data
* More meaningful 404 error message
* Fixed bugs in the API Playground

Check out the [23.06 release blog post](https://blog.opentargets.org/open-targets-platform-23-06-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 62,685 targets
* 24,713 diseases and phenotypes
* 13,210 drugs and compounds
* 15,117,741 evidence strings
* 7,835,247 target-disease associations

Visit the [Open Targets Community 23.06 release thread](https://community.opentargets.org/t/23-06-platform-release-now-live/1125) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 23.02

### Release date

22 February 2023

### Highlights

In addition to regular updates from our data providers, we have a number of new features in this release:

**New evidence for target-disease associations**

* Additional data for metabolic biomarkers added to our Gene Burden widget
* QTL-based direction of effect included in evidence from Open Targets Genetics

**Improved target annotation data**

* Integration of Target safety evidence from AOPWiki
* New data from Probes and Drugs’ 04.2022 release

**Literature updates**

* Preprints and patents now included in our bibliography

**Development updates**

* Redesigned search
* Provenance metadata

Check out the [23.02 release blog post](https://blog.opentargets.org/open-targets-platform-23-02-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 62,678 targets
* 24,713 diseases and phenotypes
* 12,854 drugs and compounds
* 10,446,771 evidence strings
* 6,656,559 target-disease associations

Visit the [Open Targets Community 23.02 release thread](https://community.opentargets.org/t/23-02-platform-release-now-live/962) for more data metrics for this release, including a per datasource breakdown of evidence strings.



## 22.11

### Release date

24 November 2022

### Highlights

In addition to continuous updates from our data providers, we have introduced the following new features:&#x20;

* Gene burden data for Parkinson’s disease
* Updated classifications for clinical trial stop reasons
* Variant functional consequences, available to browse in the Gene2Phenotype and Orphanet widgets
* Other improvements and bug fixes

Check out the [22.11 release blog post](https://blog.opentargets.org/open-targets-platform-22-11-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 62,678 targets
* 22,274 diseases and phenotypes
* 12,854 drugs and compounds
* 14,611,717 evidence strings
* 6,960,486 target-disease associations

Visit the [Open Targets Community 22.11 release thread](https://community.opentargets.org/t/22-11-platform-release-now-live/870) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 22.09

### Release date

29 September 2022

### Highlights

New data, in particular:

* Open Targets Genetics
* Genomics England PanelApp
* Gene burden
* Probes and drugs
* New data integrity file, in line with FAIR principles

Check out the[ 22.09 release blog post](https://blog.opentargets.org/open-targets-platform-22-09-release/) for more information on the new features and datasets introduced in this release.<br>

### Overall data metrics

* 61,888 targets
* 20,931 diseases and phenotypes
* 12,854 drugs and compounds
* 14,229,684 evidence strings
* 7,003,171 target-disease associations

Visit the [Open Targets Community 22.09 release thread](https://community.opentargets.org/t/22-09-platform-release-now-live/783) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 22.06

### Release date

24 June 2022

### Highlights

* New data: five additional gene burden analyses from Genebass
* New feature: new visualisation of subcellular locations of targets now available to users
*   New ontology term: “medical procedure”&#x20;



Check out the [22.06 release blog post](https://blog.opentargets.org/open-targets-platform-22-06-release/) for more information on the new features and datasets introduced in this release.&#x20;

### Overall data metrics

* 61,524 targets
* 23,074 diseases and phenotypes
* 12,854 drugs and compounds
* 14,455,104 evidence strings
* 7,247,865 target-disease associations

Visit the [Open Targets Community 22.06 release thread](https://community.opentargets.org/t/the-latest-release-22-06-is-now-live/675) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 22.04

### Release date

28 April 2022

### Highlights

* New datasource: gene burden analyses from Regeneron and the AstraZeneca
* Integration of structural variants from ClinVar
* Additional information from DailyMed drug label text-mining
* NLP classification of why clinical trials stopped
* New data: Gene2phenotype cardiac panel

Check out the[ 22.04 release blog post](https://blog.opentargets.org/open-targets-platform-22-04-release/) for more information on the new features and datasets introduced in this release.&#x20;

### Overall data metrics

* 61,524 targets
* 18,520 diseases and phenotypes
* 12,854 drugs and compounds
* 13,829,174 evidence strings
* 7,541,360 target-disease associations

Visit the [Open Targets Community 22.04 release thread](https://community.opentargets.org/t/open-targets-platform-22-04-is-out-now/555) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 22.02

### Release date

28 February 2022

### Highlights

* Gene2Phenotype terminology updated in line with the Gene Curation Coalition (GenCC)
* Data updates from a range of providers including Open Targets Genetics and ChEMBL

Check out the [22.02 release blog post](https://blog.opentargets.org/open-targets-platform-22-02-release/) for more information on the new features and datasets introduced in this release.&#x20;

### Overall data metrics

* 61,524 targets
* 18,468 diseases and phenotypes
* 12,594 drugs and compounds
* 10,880,832 evidence strings
* 7,980,448 target-disease associations

Visit the [Open Targets Community 22.02 release thread](https://community.opentargets.org/t/open-targets-platform-22-02-has-been-released/476) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 21.11

### Release date

29 November 2021

### Highlights

* New Cancer Biomarkers evidence data from the Cancer Genome Interpreter
* Updated genetic association evidence from Open Targets Genetics
* Embedded GraphQL API playground for each data table and query

Check out the [21.11 release blog post](https://blog.opentargets.org/open-targets-platform-21-11-release/) for more information on the new features and datasets introduced in this release.&#x20;

### Overall data metrics

* 60,636 targets
* 18,706 diseases and phenotypes
* 12,594 drugs and compounds
* 10,481,189 evidence strings
* 7,787,231 target-disease associations

Visit the[ Open Targets Community 21.11 release thread](https://community.opentargets.org/t/open-targets-platform-21-11-has-been-released/413) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 21.09

### Release date

30 September 2021

### Highlights

* Integration of new PROTAC tractability data from [Schneider et al. (2021)](https://doi.org/10.1038/s41573-021-00245-x)
* Integration of Genetic Constraint data from gnomAD and new Chemical Probes data from Probes & Drugs database
* Data updates from EFO, ChEMBL, and Mouse Genome Informatics
* Other improvements and bug fixes

Check out our [21.09 release blog post](https://blog.opentargets.org/open-targets-platform-21-09-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 60,636 targets
* 18,663 diseases and phenotypes
* 12,594 drugs and compounds
* 11,071,233 evidence strings
* 7,927,820 target-disease associations

Visit the [Open Targets Community 21.09 release thread](https://community.opentargets.org/t/21-09-platform-release-now-live/364) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## 21.06

### Release date

30 June 2021

### Highlights

* Updated Open Targets Genetics Portal evidence, which included the integration of FinnGen biobank data (R5) and new GWAS Catalog studies
* Integration of gene-disease data from Orphanet
* Improvements to the user interface (e.g. datatype chips on evidence page)
* Bug fixes (e.g. users can download Known Drugs table, association scores in datasets match values returned by API)

Check out our [21.06 release blog post](https://blog.opentargets.org/open-targets-platform-21-06-release/) for more information on the new features and datasets introduced in this release.

### Overall data metrics

* 60,606 targets
* 18,507 diseases and phenotypes
* 13,185 drugs and compounds
* 13,267,236 evidence strings
* 9,216,710 target-disease associations

Visit the [Open Targets Community](https://community.opentargets.org/t/21-06-platform-release-now-live/244) for more data metrics for this release, including a per datasource breakdown of evidence strings.

## Archive

For release notes for previous releases, check out the [Open Targets Community News & Announcement section](https://community.opentargets.org/c/news-and-announcements/5).
