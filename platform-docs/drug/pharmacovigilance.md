---
description: Data describing pharmacovigilance annotation for the drug
---

# Pharmacovigilance

## Overview

Before approval, new therapeutic drug treatments are extensively tested in clinical trials. However, some of the side effects are only identified when prescribed to larger cohorts of patients, with one or more medical conditions, for a sustained period of time or in combination with other treatments.

For this reason, regulatory agencies—for example, the Food & Drug Administration or the European Medicines Agency—provide pharmacovigilance programs to monitor and survey Adverse Drug Reactions (ADRs).

## Data sources

### FDA Adverse Event Reporting System (FAERS) <a href="#hero-title" id="hero-title"></a>

The FDA Adverse Event Reporting System (FAERS) – [https://open.fda.gov/data/faers](https://open.fda.gov/data/faers/) – is a database that contains millions of public reports with information on adverse event and medication error reports submitted to FDA. The database is designed to support the FDA's post-marketing safety surveillance program for drug and therapeutic biologic products. Adverse events and medication errors are mapped to terms in the Medical Dictionary for Regulatory Activities (MedDRA) terminology.

## Computational pipelines and datasets

While recurrence of a given adverse event is relevant, it's the specificity of the event to the drug what might flag concerns. In order to get a list of significant drug–ADRs associations, we have implemented an analysis similar to the one described by [Maciejewski et al. (2017)](https://europepmc.org/abstract/MED/28786378).

First we apply a set of filters to the reports as described below:

* Only reports submitted by health professionals (_primarysource.qualification in (1,2,3)_)
* Exclude reports that resulted in death (no entries with _seriousnessdeath=1_)
* Only drugs that were considered by the reporter to be the cause of the event _(drugcharacterization=1)_
* Remove [blacklisted](https://github.com/opentargets/platform-etl-openfda-faers/blob/master/src/main/resources/blacklisted_events.txt) events curated manually to exclude uninformative events

Next, we sought to map the drugs in the FAERS reports to the drugs in the Open Targets Platform (ChEMBL IDs). Any of the above listed fields were used when exact matches were available:

| FAERS drugs                   | Open Targets Platform drugs |
| ----------------------------- | --------------------------- |
| `drug.medicinalproduct`       | `drug.medicinalproduct`     |
| `drug.openfda.generic_name`   | `synonyms`                  |
| `drug.openfda.brand_name`     | `pref_name`                 |
| `drug.openfda.substance_name` | `trade_names`               |

The significant drug–ADR pairs were then evaluated using the Likelihood Ratio Test (LRT) as previously described by [Huang et al. (2011)](https://europepmc.org/abstract/MED/23331230). The significance of a given drug–ADR is implicitly corrected by how often a drug is found in a report and how often an event is reported across drugs. This way, we prevent the drug–ADR associations to be biased by overrepresented ADRs (e.g. headache, nausea) or drugs (e.g. paracetamol, ibuprofen). In order to assess significance, an LRT critical value for every drug is calculated using an empirical Monte Carlo simulation, similar to the one implemented by [openFDA](https://openfda.shinyapps.io/LRTest/_w_c5c2d04d/lrtmethod.pdf).

Due to the nature of the surveillance reports, it's relatively common for the indication for which a drug was prescribed to appear in the list of significant ADRs. Given the current structure of the data provided in a FAERS report, we cannot distinguish whether it's a problem with the dosage the drug was prescribed or an excessive phenotypic characterisation of the patient in the report.

All pharmacovigilance data is available for download on [our data downloads page](https://platform.opentargets.org/downloads).

## Publications

Huang L, Zalkikar J, Tiwari RC. **Likelihood ratio test-based method for signal detection in drug classes using FDA's AERS database**. J Biopharm Stat. 2013;23(1):178-200. doi: [10.1080/10543406.2013.736810](https://doi.org/10.1080/10543406.2013.736810). PMID: [23331230](https://pubmed.ncbi.nlm.nih.gov/23331230/).

Maciejewski M, Lounkine E, Whitebread S, Farmer P, DuMouchel W, Shoichet BK, Urban L. **Reverse translation of adverse event reports paves the way for de-risking preclinical off-targets**. Elife. 2017 Aug 8;6:e25818. doi: [10.7554/eLife.25818](https://doi.org/10.7554/elife.25818). PMID: [28786378](https://pubmed.ncbi.nlm.nih.gov/28786378/); PMCID: [PMC5548487](https://europepmc.org/article/PMC/PMC5548487).
