---
description: >-
  Overview of the technical infrastructure that supports the Open Targets
  Platform
---

# Platform infrastructure

## Introduction

The Open Targets Platform infrastructure stack is composed of multiple elements:

1. Data and evidence generation pipelines
2. Evidence processing and scoring ETL pipelines
3. Globally-distributed GraphQL API
4. Terraform deployment
5. Robust, optimised front-end user interface

## GitHub repositories

### Data and evidence

* [evidence\_datasource\_parsers](https://github.com/opentargets/evidence_datasource_parsers): internal pipelines used to generate evidence
* [json\_schema](https://github.com/opentargets/json_schema): evidence object schema used for evidence and association scoring
* [OnToma](https://github.com/opentargets/OnToma): Python module to map disease or phenotype terms to EFO

### Extract, transform, load (ETL)

* [platform-input-support](https://github.com/opentargets/platform-input-support): scripts that process and prepare data for our ETL pipelines
* [platform-etl-backend](https://github.com/opentargets/platform-etl-backend): ETL pipelines to generate associations, evidence, and entity indices
* [platform-etl-openfda-faers](https://github.com/opentargets/platform-etl-openfda-faers): ETL pipeline to process Open FDA adverse events data
* [platform-etl-literature](https://github.com/opentargets/platform-etl-literature): ETL pipeline to generate similar entities and publications
* [platform-output-support](https://github.com/opentargets/platform-output-support): scripts for infrastructure tasks and generating a Platform release

### API

* [platform-api](https://github.com/opentargets/platform-api): GraphQL API

### Deployment

* [terraform-google-opentargets-platform](https://github.com/opentargets/terraform-google-opentargets-platform): scripts to deploy the public version of the Platform

### Front-end

* [platform-app](https://github.com/opentargets/platform-app): front-end web interface

## Open source contributions

As a consortium committed to developing open-source, freely available tools that support systematic drug target identification and prioritisation, we actively encourage and accept open source contributions to our various repositories.

Please review [our contribution guidelines](https://github.com/opentargets/platform/blob/master/Contribution%20Guidelines.md) and check out the [Open Targets Community](https://community.opentargets.org) to get started.

If you have further questions, please get in touch with us on the [Open Targets Community](https://community.opentargets.org/).
