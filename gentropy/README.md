---
description: Open Targets post-GWAS analysis pipelines
---

# GWAS & functional genomics

The Platform is built upon a significant effort to analyse genome-wide associations studies and interpret them in the context of functional genomics studies. This effort to inform target identification and prioritisation datasets leverages [gentropy](gentropy.md) a highly-scalable python framework for post-GWAS analysis.

A more detailed view on the data and methodology is available in:

* [Data sources](data-sources.md) used to ingest variant annotation, GWAS and functional genomics information.&#x20;
* [Fine-mapping](fine-mapping.md) pipelines to identify likely causal variants in GWAS-significant signals in different sources.
* [Interval](intervals.md) dataset to connect variants to genes using epigenetics datasets.
* [Colocalisation](colocalisation.md) performed on overlapping GWAS and molQTL credible sets.
* [Locus-to-Gene](locus-to-gene-l2g.md) predictions to assess likely causal genes near identified credible sets.

