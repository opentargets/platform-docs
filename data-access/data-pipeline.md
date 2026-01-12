---
description: >-
  The Open Targets data pipeline is a complex process orchestrated in Apache
  Airflow, and it is divideded into data acquisition, transformation and data
  output.
---

# Data pipeline

## Introduction

The data pipeline is composed of multiple elements:

1. Data and evidence generation processes
2. Input stage
3. Transformation stage and ETL processes
4. Output stage
5. Gentropy-specific processes
6. Orchestration

## GitHub repositories

### Data and evidence

* [curation](https://github.com/opentargets/curation) — Open Targets curation repository
* [evidence\_datasource\_parsers](https://github.com/opentargets/evidence_datasource_parsers) — internal pipelines used to generate evidence
* [json\_schema](https://github.com/opentargets/json_schema) — evidence object schema used for evidence and association scoring
* [OnToma](https://github.com/opentargets/OnToma) — Python module to map disease or phenotype terms to EFO

### Gentropy

* [gentropy](https://github.com/opentargets/gentropy) — Open Targets' genomics toolkit

See [here](https://app.gitbook.com/o/-LC3OlEMulAutIN2QOro/s/-MU4dMxOmLaVNWfVNvpC/~/changes/506/gentropy) for more info on the Gentropy pipelines.&#x20;

### Orchestration&#x20;

* [orchestration](https://github.com/opentargets/orchestration) — Open Targets data pipelines orchestrator

See detailed orchestration documentation [here](https://github.com/opentargets/orchestration/tree/dev/docs).

The Platform ETL (“extract, transform, and load”) and the [Genetics ETL](https://app.gitbook.com/o/-LC3OlEMulAutIN2QOro/s/-MU4dMxOmLaVNWfVNvpC/~/changes/506/gentropy#genetics-etl) were separate processes before, but they are now merged into one single pipeline. This means that the data produced for both Genetics ETL and the Platform are released at the same time. Herein, we refer to this joint pipeline as the "unified pipeline".

The orchestration occurs on Google Airflow using Google Cloud as the cloud resource provider. The logic of the orchestration is based on the steps. The combination of steps forms directed acyclic graphs (DAGs).&#x20;

<figure><img src="../.gitbook/assets/Schemas and figures.jpg" alt=""><figcaption><p>Schematic overview of Open Targets pipelines</p></figcaption></figure>

The unified pipeline uses many [static assets](https://app.gitbook.com/o/-LC3OlEMulAutIN2QOro/s/-MU4dMxOmLaVNWfVNvpC/~/changes/506/gentropy#static-assets) (link), like Open Targets related data and data needed to run Genetics ETL.

### Unified pipeline&#x20;

* [otter](https://github.com/opentargets/otter) — **O**pen **T**argets' **T**ask **E**xecuto**R** i.e. scripts that process and prepare data for our ETL pipelines
* [platform-etl-backend](https://github.com/opentargets/platform-etl-backend): ETL pipelines to generate associations, evidence, and entity indices
* [platform-etl-openfda-faers](https://github.com/opentargets/platform-etl-openfda-faers): ETL pipeline to process Open FDA adverse events data
* [platform-etl-literature](https://github.com/opentargets/platform-etl-literature): ETL pipeline to generate similar entities and publications
* [platform-output-support](https://github.com/opentargets/platform-output-support): scripts for infrastructure tasks and generating a Platform release

If you have further questions, please get in touch with us on the [Open Targets Community](https://community.opentargets.org/).
