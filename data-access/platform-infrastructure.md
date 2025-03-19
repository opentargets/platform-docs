---
description: >-
  Overview of the technical infrastructure that supports the Open Targets
  Platform
---

# 🆕 Platform infrastructure

## Introduction

The Open Targets Platform infrastructure stack is composed of three layers, data, backend and frontend.

1. Data layer
   1. Opensearch — Contains the bulk of the data
   2. Clickhouse — Contains data related to associations view
2. Backend layer
   1. API — The main backend application, providing the GraphQL engine
   2. OpenAI-API — The summarizing engine for literature section
3. Frontend layer
   1. Web — A React SPA web application

<figure><img src="../.gitbook/assets/infra.drawio.svg" alt="" width="563"><figcaption></figcaption></figure>

Currently this infrastructure is hosted on Google Cloud, using a load-balanced, globally distributed and highly scalable deployment based on Terraform.

## GitHub repositories

### Backend

* [platform-api](https://github.com/opentargets/platform-api) — GraphQL API
* [ot-ai-api](https://github.com/opentargets/ot-ai-api) — OpenAI API router

### Frontend

* [ot-ui-apps](https://github.com/opentargets/ot-ui-apps) — Open Targets web applications

### Deployment

* [terraform-google-opentargets](https://github.com/opentargets/terraform-google-opentargets-platform) — Open Targets Infrastructure definition, scripts in charge of setting up the data layer with the relevant disk images and spinning up the rest of the infrastructure.

## Open source contributions

As a consortium committed to developing open-source, freely available tools that support systematic drug target identification and prioritisation, we actively encourage and accept open source contributions to our various repositories.

Please review [our contribution guidelines](https://github.com/opentargets/platform/blob/master/Contribution%20Guidelines.md) and check out the [Open Targets Community](https://community.opentargets.org) to get started.

If you have further questions, please get in touch with us on the [Open Targets Community](https://community.opentargets.org/).
