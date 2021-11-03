# Drug

## Overview

A drug in the platform is understood as any bioactive molecule with drug-like properties as defined in the EMBL-EBI [ChEMBL](https://www.ebi.ac.uk/chembl/) database.

A drug in the Platform might belong to different modalities, including small molecules, antibodies or oligonucleotides among others. However, some biologic therapies such as vaccines, blood products or cell therapies are not represented in our drug set. Moreover, the molecule-centric definition implies multi-ingredient drugs won't be represented and only their individual active moieties might be available on the site.

The ChEMBL representation of drugs distinguishes **parent** bioactive molecules from the **child** molecule, which contain a modified (e.g. salt) version of the same active ingredient. Both parent and child molecules are included in the Platform.

{% embed url="https://www.youtube.com/watch?v=2cHctti3aIQ" %}

## Drug annotation data sources

| Annotation data                                                                                           | Data source                                                                                                     |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Molecule information, Indications, Mechanisms of action, Drug warnings (black box and withdrawn warnings) | [ChEMBL ](https://www.ebi.ac.uk/chembl/)                                                                        |
| [Pharmacovigilance](pharmacovigilance.md)                                                                 | [FAERS](https://www.fda.gov/drugs/surveillance/questions-and-answers-fdas-adverse-event-reporting-system-faers) |
| [Bibliography](../bibliography.md)                                                                        | [Open Targets](../bibliography.md)                                                                              |
