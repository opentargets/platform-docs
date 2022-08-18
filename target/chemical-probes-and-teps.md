# Chemical probes & TEPs

## Overview

To support further assessments about the suitability of targets for a discovery pipeline, the Open Targets Platform integrates information from various sources on chemical probes and Target Enabling Packages (TEPs).

### Chemical probes

A chemical probe is a small molecule that can act as chemical modulator of a system, such as a cell or an organism, by reversibly binding to a biological target. Chemical probes are expected to have a minimum standard of high affinity, binding selectivity and efficacy. As opposed to drugs, chemical probes do not need to meet the same requirements in terms of pharmacokinetics, pharmacodynamics, and bioavailability.

### Target Enabling Packages

Target Enabling Packages (TEPs) are a critical mass of reagents and knowledge allowing for the rapid biochemical and chemical exploration of a given target.

As noted by the [Structural Genomics Consortium](https://www.thesgc.org/tep), each TEP contains:

* Protein production methods
* Biochemical/biophysical assays for activity, affinity
* Structures of the protein, potentially including wild type and disease mutant proteins; full-length or domains; protein-ligand complexes; structures of close homologues
* Initial chemical matter from a fragment or small molecule screen

Additional components of TEPs may be developed on a case-by-case basis, based upon reasonable scientific need, in collaboration with TEP target nominators:

* An antibody or nanobody
* Cell-based assay
* CRISPR knockout

## Data sources

### Probes & Drugs Portal

The Probes & Drugs Portal - [https://www.probes-drugs.org/home/](https://www.probes-drugs.org/home/) - is a public resource joining together focused libraries of bioactive compounds (probes, drugs, specific inhibitor sets etc.) with commercially available screening libraries. The purpose of the Portal is to reflect the current state of bioactive compound space and to enable its exploration from different points of view. It is intended to serve as a central hub in chemical biology research by providing a unique integration of the most relevant probes sources such as the [Chemical Probes Portal](https://www.chemicalprobes.org), [Open Science Probes](https://www.sgc-ffm.uni-frankfurt.de), and [ProbeMiner](https://probeminer.icr.ac.uk).

### Structural Genomics Consortium

The Structural Genomics Consortium (SGC) - [https://www.thesgc.org/](https://www.thesgc.org) - is a public-private partnership focused on accelerating drug discovery using open science. The SGC’s core research operations are funded by pharmaceutical companies, governments, and charities, all of which act as research partners and participate in the governance of the SGC.

## Computational pipelines and datasets

Chemical probes datasets are downloaded from each data source listed above, mapped to the correct Ensembl gene ID, and ingested during our initial pipeline steps. The data is available for download as part of the target core annotation from [our data download page](https://platform.opentargets.org/downloads).
