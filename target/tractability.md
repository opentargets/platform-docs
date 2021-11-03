---
description: >-
  Data for assessing tractability with small molecule, antibody, and other
  clinical modalities
---

# Tractability

## Overview

To support target prioritisation, the Open Targets Platform includes tractability data that identifies key details, including if there is a binding site suitable for small molecule binding, an accessible epitope for antibody based therapy, relevant data for using Proteolysis Targeting Chimeras (PROTACs), or a compound in clinical trials with a modality other than small molecule or antibody.&#x20;

The tractability data can assist in target prioritisation by identifying potential drug targets suitable for discovery pipelines and therapeutic modalities that are most likely to succeed. It also supports further investigation of targets for which there are no ligands or experimental structures or those targets outside a "druggable" target family but with strong genetic associations.

Our target tractability is based on a modified version of [Approaches to target tractability assessment – a practical perspective](https://pubs.rsc.org/en/content/articlelanding/2018/md/c7md00633k#!divAbstract) and [The PROTACtable genome](https://doi.org/10.1038/s41573-021-00245-x) and has workflows that generate tractability assessments for small molecule (SM), antibody (AB), Proteolysis Targeting Chimeras (PR), and other clinical (OC) modalities.&#x20;

## Computational pipeline and datasets

The tractability assessments displayed on the Platform's target profile pages is the result of an [open-source computational pipeline](https://github.com/melschneider/tractability\_pipeline\_v2/tree/master/ot\_tractability\_pipeline\_v2) that performs _in silico_ tractability assessments with small molecule, antibody, PROTAC, and other clinical modality workflows.&#x20;

Data sources used in the pipeline include UniProt, HPA, PDBe, DrugEBIlity, ChEMBL, Pfam, InterPro, Complex Portal, DrugBank, Gene Ontology, and BioModels.&#x20;

Tractability data for each target is available in the `target` dataset available for download on [our data downloads page](https://platform.opentargets.org/downloads).

Alternatively, you can also download the input TSV file with the per-target assessments via FTP. To access this file, visit [our FTP site](http://ftp.ebi.ac.uk/pub/databases/opentargets/platform/) and click on the release version (e.g. 21.04), followed by "input", followed by "annotation-files". You can then download the `tractability_buckets` TSV file. Descriptions of the columns found in the input file can be found on the [pipeline README.md file](https://github.com/melschneider/tractability\_pipeline\_v2/blob/master/README.md).

## Publications

Brown KK, Hann MM, Lakdawala AS, Santos R, Thomas PJ, Todd K. **Approaches to target tractability assessment - a practical perspective**. Medchemcomm. 2018 Feb 14;9(4):606-613. doi: [10.1039/c7md00633k](https://doi.org/10.1039/c7md00633k). PMID: [30108951](https://pubmed.ncbi.nlm.nih.gov/30108951/); PMCID: [PMC6072525](https://europepmc.org/article/PMC/PMC6072525).

Schneider M, Radoux CJ, Hercules A, Ochoa D, Dunham I, Zalmas LP, Hessler G, Ruf S, Shanmugasundaram V, Hann MM, Thomas PJ, Queisser MA, Benowitz AB, Brown K, Leach AR. **The PROTACtable genome**. Nat Rev Drug Discov. 2021 Jul 20. doi: [10.1038/s41573-021-00245-x](https://doi.org/10.1038/s41573-021-00245-x). PMID: [34285415](https://pubmed.ncbi.nlm.nih.gov/34285415/).
