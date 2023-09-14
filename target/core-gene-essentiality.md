---
description: Data supporting core essentiality of a target
---

# Core Gene Essentiality

## Overview

Core essential target genes are unlikely to tolerate inhibition and susceptible to causing adverse events if modulated. This is crucial safety information for drug discovery scientists looking to develop inhibition strategies.

To support target prioritisation with an extra focus on target safety, the Open Targets Platform includes key information on target core essentiality in the context of 28 tissues assayed in the [DepMap portal](https://depmap.org/portal/). In this project and its ancillary projects (e.g. [Achilles](https://depmap.org/portal/achilles/)), cell fitness is measured after the inhibition of individual genes across a number of cell lines. As a result, a gene is catalogued as core essential If the majority of cell lines die after inhibition/knockout. Although in cancer, this experiment represents a good proxy of whether loss-of-functions are tolerated across a diverse set of tissues.

**Essentiality assessment:** The [Chronos dependency score](https://depmap.org/portal/gene/KIT?tab=dependency) is based on data from a cell depletion assay. A lower Chronos score indicates a higher likelihood hat the gene of interest is essential in a given cell line. A score of 0 indicates a gene is not essential; correspondingly -1 is comparable to the median of all pan-essential genes.&#x20;

Together with a DepMap target annotation widget, essential target genes are annotated with a \`Core essential gene\` chip on the target page.

## **Data source**

### DepMap Portal

The goal of the Dependency Map ([DepMap](https://depmap.org/portal/)) portal is to empower the research community to make discoveries related to cancer vulnerabilities by providing open access to key cancer dependencies analytical and visualisation tools.

## Publications

When using this data please remember to acknowledge the sources:

[Pacini, C et al 2021](https://www.nature.com/articles/s41467-021-21898-7)

You can find all the relevant DepMap Publications [here](https://depmap.org/portal/home/#/publications)
