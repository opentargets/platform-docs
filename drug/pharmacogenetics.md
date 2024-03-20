---
description: Data supporting pharmacogenetics annotation for a drug
---

# Pharmacogenetics

## Overview

Pharmacogenetics is the study of how genetic variation may change your response to a specific drug. Through the integration of pharmacogenetics data into the Platform, our objective is to apply clinical annotations available in the Pharmacogenetics KnowledgeBase (PharmGKB) to aid target prioritisation for drug discovery. We also enhance these annotations by adding detailed annotations on variant consequence prediction, drug response categories, and specific drug information and whether the gene is a direct target of the drug. This process involves applying advanced phenotype extraction techniques to offer a refined representation of phenotypes, thereby providing a more precise understanding of the genetic determinants influencing treatment outcomes.

## Data sources

[PharmGKB](https://www.pharmgkb.org/) is an NIH-funded comprehensive resource that provides information about how human genetic variation affects response to medications. PharmGKB collects, curates and disseminates knowledge about clinically actionable gene-drug associations and genotype-phenotype relationships, focusing on the impact of genetic variation on drug response for clinicians and researchers.

We have modelled and harmonised the data from the[ ](https://www.pharmgkb.org/clinicalAnnotations)[Clinical Annotation](https://www.pharmgkb.org/clinicalAnnotations) section of PharmGKB, which provides information about variant-drug pairs based upon collating and summarising variant annotations. Variant annotations are curated manually from a scientific publication. Clinical Annotations then provide an overarching summary and curated [level of evidence](https://www.pharmgkb.org/page/clinAnnLevels) for the association between a genetic variant and particular drug responses based on multiple variant annotations. The likely consequence for each genotype of the variant on drug response is represented, in comparison to the other genotypes of that variant.

We have also included annotations for star (\*) alleles, a nomenclature used in the pharmacogenetics field for representing key functional variants involved in drug responses.

## Publications

When using this data please remember to acknowledge the sources:

[Michelle Whirl-Carrillo et al, 2021](https://pubmed.ncbi.nlm.nih.gov/34216021/)

[Michelle Whirl-Carrillo et al, 2012 ](https://pubmed.ncbi.nlm.nih.gov/22992668/)

You can find all the relevant PharmGKB Publications[ here](https://www.pharmgkb.org/page/citingPharmgkb)
