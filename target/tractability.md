---
description: >-
  Data for assessing tractability with small molecule, antibody, and other
  clinical modalities
---

# Tractability

## Overview

To support target prioritisation, the Open Targets Platform includes tractability data that identifies key details, including if there is a binding site suitable for small molecule binding, an accessible epitope for antibody based therapy, relevant data for using Proteolysis Targeting Chimeras (PROTACs), or a compound in clinical trials with a modality other than small molecule or antibody.

The tractability data can assist in target prioritisation by identifying potential drug targets suitable for discovery pipelines and therapeutic modalities that are most likely to succeed. It also supports further investigation of targets for which there are no ligands or experimental structures or those targets outside a "druggable" target family but with strong genetic associations.

Our target tractability is based on a modified version of [Approaches to target tractability assessment – a practical perspective](https://pubs.rsc.org/en/content/articlelanding/2018/md/c7md00633k#!divAbstract) and [The PROTACtable genome](https://doi.org/10.1038/s41573-021-00245-x) and has workflows that generate tractability assessments for small molecule (SM), antibody (AB), Proteolysis Targeting Chimeras (PR), and other clinical (OC) modalities.

## Assessments

The tractability assessments displayed on the Platform's target profile pages is the result of an [open-source computational pipeline](https://github.com/melschneider/tractability\_pipeline\_v2/tree/master/ot\_tractability\_pipeline\_v2) that performs _in silico_ tractability assessments with small molecule, antibody, PROTAC, and other clinical modality workflows.

Data sources used in the pipeline include UniProt, HPA, PDBe, DrugEBIlity, ChEMBL, Pfam, InterPro, Complex Portal, DrugBank, Gene Ontology, and BioModels.

Assessments common to all modalities, ingested from ChEMBL, are:&#x20;

* **Approved Drug**: the target has clinical precedence with Phase IV drugs;&#x20;
* **Advanced Clinical**: the target has clinical precedence with Phase II or III drugs;
* **Phase 1 Clinical**: the target has clinical precedence with Phase I drugs.&#x20;

We also include additional assessments specific to each modality.

### Small molecule

* **Structure with Ligand**: Target has been co-crystallised with a small molecule (source: [Protein Data Bank](https://www.rcsb.org/))
* **High-Quality Ligand**: Target with ligand(s) (PFI ≤ 7, SMART hits ≤ 2, scaffolds ≥ 2) (source: [ChEMBL](https://www.ebi.ac.uk/chembl/))
* **High-Quality Pocket**: Target has a DrugEBIlity score of ≥ 0.7 (source: [DrugEBIlity](http://chembl.github.io/drugebility-structure-based-component/))
* **Med-Quality Pocket**: Target has a DrugEBIlity score between 0 and 0.7 (source: [DrugEBIlity](http://chembl.github.io/drugebility-structure-based-component/))
* **Druggable Family**: Target is considered druggable as per [Finan et al](https://pubmed.ncbi.nlm.nih.gov/28356508/)’s Druggable Genome pipeline.

### Antibody

* **UniProt loc high conf:** High confidence that the subcellular location of the target is either plasma membrane, extracellular region/matrix, or secretion (source: [Uniprot](https://www.uniprot.org/))
* **GO CC high conf:** High confidence that the subcellular location of the target is either plasma membrane, extracellular region/matrix, or secretion (source: [Gene Ontology](http://geneontology.org/))
* **UniProt loc med conf:** Medium confidence that the subcellular location of the target is either plasma membrane, extracellular region/matrix, or secretion (source: [Uniprot](https://www.uniprot.org/))
* **UniProt SigP or TMHMM**: Target has a predicted signal peptide or trans-membrane regions, and not destined to organelles (source: Uniprot SigP, [TMHMM](https://services.healthtech.dtu.dk/service.php?TMHMM-2.0))
* **GO CC med conf:** Medium confidence that the subcellular location of the target is either plasma membrane, extracellular region/matrix, or secretion (source: [Gene Ontology](http://geneontology.org/))
* **Human Protein Atlas loc:** High confidence that the target is located in the Plasma membrane (source: [HPA](https://www.proteinatlas.org/))

### PROTAC

* **Literature**: Target mentioned in a set of manually curated PROTAC-related publications (source: [Europe PMC](http://europepmc.org/))
* **UniProt Ubiquitination:** Target tagged with the Uniprot keyword “Ubl conjugation \[KW-0832]”, which indicates that the protein has a ubiquitination site, based on evidence from the literature **** (source: [Uniprot](https://www.uniprot.org/))
* **Database Ubiquitination:** Target has reported ubiquitination sites in [PhosphoSitePlus](https://www.phosphosite.org/homeAction.action), [mUbiSiDa](http://reprod.njmu.edu.cn/cgi-bin/mubisida/mUbiSiDa.php) (2013), or [Kim et al. 2011](https://www.sciencedirect.com/science/article/pii/S1097276511006757)
* **Half-life Data:** Target has available half-life data (source: [Mathieson et al. 2018](https://www.nature.com/articles/s41467-018-03106-1))
* **Small Molecule Binder:** Target has a reported small-molecule ligand in ChEMBL with a measured activity of at least 10 μM in a target-based assay (source: [ChEMBL](https://www.ebi.ac.uk/chembl/))

## Computational pipeline and datasets

Tractability data for each target is available in the `target` dataset available for download on [our data downloads page](https://platform.opentargets.org/downloads).

Alternatively, you can also download the input TSV file with the per-target assessments via FTP. To access this file, visit [our FTP site](http://ftp.ebi.ac.uk/pub/databases/opentargets/platform/) and click on the release version (e.g. 21.04), followed by "input", followed by "annotation-files". You can then download the `tractability_buckets` TSV file. Descriptions of the columns found in the input file can be found on the [pipeline README.md file](https://github.com/melschneider/tractability\_pipeline\_v2/blob/master/README.md).

## Publications

Brown KK, Hann MM, Lakdawala AS, Santos R, Thomas PJ, Todd K. **Approaches to target tractability assessment - a practical perspective**. Medchemcomm. 2018 Feb 14;9(4):606-613. doi: [10.1039/c7md00633k](https://doi.org/10.1039/c7md00633k). PMID: [30108951](https://pubmed.ncbi.nlm.nih.gov/30108951/); PMCID: [PMC6072525](https://europepmc.org/article/PMC/PMC6072525).

Schneider M, Radoux CJ, Hercules A, Ochoa D, Dunham I, Zalmas LP, Hessler G, Ruf S, Shanmugasundaram V, Hann MM, Thomas PJ, Queisser MA, Benowitz AB, Brown K, Leach AR. **The PROTACtable genome**. Nat Rev Drug Discov. 2021 Jul 20. doi: [10.1038/s41573-021-00245-x](https://doi.org/10.1038/s41573-021-00245-x). PMID: [34285415](https://pubmed.ncbi.nlm.nih.gov/34285415/).
