# Target

## Overview

A target in the Platform is understood as any naturally-occurring molecule that can be targeted by a medicinal product. EMBL-EBI's [Ensembl](https://www.ensembl.org) database is used as source for human targets in the Platform, with the Ensembl gene ID as the primary identifier.&#x20;

Criteria for target inclusion:

* Genes from all biotypes encoded in canonical chromosomes
* Genes in alternative assemblies encoding for a reviewed protein product.

This definition accounts for some of the complexities of human targets; targets are not only protein coding genes, RNAs or pseudogenes are also considered. However, the current definition has some potential drawbacks. Some drug targets are the result of interactions between genes (e.g. gene fusion) or proteins (e.g. protein complexes). The current target entity does not yet consider these cases, which will be addressed in the future.

{% embed url="https://www.youtube.com/watch?v=iYRCGRGI5K4" %}

## Target annotation data sources

| Annotation data                                                                                  | Data source                                                                                                                                                            |
| ------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Protein, positional, and structural information (ProtVista); Subcellular location; Gene Ontology | [UniProt](https://www.uniprot.org)                                                                                                                                     |
| [Molecular interactions](molecular-interactions.md)                                              | [Open Targets](molecular-interactions.md)                                                                                                                              |
| Pathways                                                                                         | [Reactome](https://reactome.org)                                                                                                                                       |
| [Baseline expression](baseline-expression.md)                                                    | [Expression Atlas](https://www.ebi.ac.uk/gxa/home); [GTEx](https://www.gtexportal.org/home/documentationPage); [Human Protein Atlas](http://www.proteinatlas.org)      |
| Comparative genomics                                                                             | [Ensembl Compara](https://www.ensembl.org/info/docs/api/compara/index.html)                                                                                            |
| Mouse phenotypes                                                                                 | [MGI](http://www.informatics.jax.org/phenotypes.shtml)                                                                                                                 |
| Cancer hallmarks                                                                                 | [Cancer Gene Census](https://cancer.sanger.ac.uk/census)                                                                                                               |
| [Chemical Probes](chemical-probes-and-teps.md)                                                   | [Probes & Drugs](https://www.probes-drugs.org)                                                                                                                         |
| [Bibliography](../bibliography.md)                                                               | [Open Targets](../bibliography.md)                                                                                                                                     |
| [Target tractability](tractability.md)                                                           | [Open Targets](tractability.md)                                                                                                                                        |
| [Target safety](safety.md)                                                                       | [ToxCast](https://www.epa.gov/chemical-research/toxicity-forecasting), [AOPWiki](https://aopwiki.org), [PharmGKB](https://www.pharmgkb.org/) and selected publications |
| [Target Enabling Packages (TEPs)](chemical-probes-and-teps.md)                                   | [SGC](https://www.thesgc.org/tep)                                                                                                                                      |
| Known drugs                                                                                      | [ChEMBL](https://www.ebi.ac.uk/chembl/)                                                                                                                                |
| CRISPR-Cas9 cancer cell line dependency                                                          | [Project Score](https://score.depmap.sanger.ac.uk)                                                                                                                     |
| [Core Gene Essentiality](https://platform-docs.opentargets.org/target/core-gene-essentiality)    | [DepMap Portal](https://depmap.org/portal/)                                                                                                                            |
| [Pharmacogenetics](https://platform-docs.opentargets.org/target/pharmacogenetics)                | [ClinPGx](https://www.clinpgx.org/)                                                                                                                                    |
| Genetic constraint                                                                               | [gnomAD](https://gnomad.broadinstitute.org)                                                                                                                            |
| 95% Molecular QTL credible sets                                                                  | [Open Targets ](../gentropy/fine-mapping.md)                                                                                                                           |
