# Drug

## Overview

A drug in the Platform is understood as any bioactive molecule with drug-like properties as defined in the EMBL-EBI [ChEMBL](https://www.ebi.ac.uk/chembl/) database.

To further refine how we define a drug in the Platform, we subset ChEMBL's drugbase to capture molecules that meet the following criteria:

* Drugs for which the indication is known
* Drugs for which the target they modulate is identified
* Drugs that are listed in DrugBank
* Drugs that are acknowledged as chemical probes

A drug in the Platform might belong to different modalities, including small molecules, antibodies, or oligonucleotides among others. However, some biologic therapies such as vaccines, blood products, or cell therapies are not represented in our drug set. Moreover, the molecule-centric definition implies multi-ingredient drugs won't be represented and only their individual active moieties might be available on the site.

In the ChEMBL representation of drugs, a clear distinction is made between parent bioactive molecules and their corresponding child molecules. **Parent molecules** encompass the original, unmodified form of the active ingredient, while **child molecules** refer to modified versions, such as salts. In the Platform, both parent and child molecules are included, ensuring comprehensive coverage of the drug landscape.

When it comes to data propagation, parent molecules retain their own distinct information, as well as aggregate the specific details from all their child molecules. On the other hand, child molecules solely capture their own individual information, without incorporating any data from other molecules. This consistent approach extends to various aspects, including indications, mechanism of action, and drug warnings. By adopting this systematic framework, our Platform facilitates accurate representation and analysis of the diverse molecular entities and their associated properties.

{% embed url="https://www.youtube.com/watch?v=2cHctti3aIQ" %}

## Drug annotation data sources

| Annotation data                                                                                                                | Data source                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| Molecule information, Indications, Mechanisms of action, Drug warnings (black box and withdrawn warnings)                      | [ChEMBL](https://www.ebi.ac.uk/chembl/)                                                                         |
| [Pharmacovigilance](pharmacovigilance.md)                                                                                      | [FAERS](https://www.fda.gov/drugs/surveillance/questions-and-answers-fdas-adverse-event-reporting-system-faers) |
| [Pharmacogenetics ](https://app.gitbook.com/o/-LC3OlEMulAutIN2QOro/s/-MU4dMxOmLaVNWfVNvpC/~/changes/445/drug/pharmacogenetics) | [PharmGKB](https://www.pharmgkb.org/)                                                                           |
| [Bibliography](../bibliography.md)                                                                                             | [Open Targets](../bibliography.md)                                                                              |
