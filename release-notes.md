---
description: Summary of release highlights for the Open Targets Platform
---

# Release notes

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
* Strengthened search functionality with performance optimisations and additional filtering capabilities.

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

Check out the[ 22.09 release blog post](https://blog.opentargets.org/open-targets-platform-22-09-release/) for more information on the new features and datasets introduced in this release.\


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
