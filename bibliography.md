---
description: >-
  Computational pipeline generating lists of publications based on similar
  entities
---

# Bibliography

## Overview

The Platform Bibliography tool aims to provide context on the scientific background available in the literature regarding the target, disease or phenotype or drug entities of interest. The Platform aims to provide not only what publications have referenced the entities of interest, but also what other entities frequently occur in the literature in conjunction with the entities of interest. Open Targets has developed in collaboration with Europe PMC a pipeline that tries to maximise the literature information extraction by using a combination of Natural Entity Recognition, ontological normalisation and data analysis.

## Data sources

### Europe PMC

Europe PMC (EPMC) - [https://europepmc.org](https://europepmc.org/About) - is an open science database that facilitates access to a comprehensive collection of life science publications, preprints, and patents. Europe PMC provides researchers with freely available data available through their website, APIs, and bulk downloads.

In conjunction with the EPMC corpus, all the information required to build the Platform entities is required in order to establish a dictionary of terms and synonyms associated with each entity.

## Computational pipeline and datasets

#### Natural entity recognition (NER)

A machine learning model trained using BioBERT and a combination of curated datasets is applied on the EPMC corpus formed by abstracts and full-text articles. The model tags every gene-protein (GP), disease (DS) or drug (DR) entity in every publication. The resulting set provides some metadata on the publications, the sections where the matches are found and the sentences, where more than one type of entity co-occur.

#### Entity normalisation

In order to ground the tagged text to the Platform entities, a dictionary-based approach is applied to the tagged entities by applying a series of standard Natural Language Processing tools (e.g. stemming, stop-words, etc.). As a result, a fraction of the tagged sentences are grounded to the Platform entities and annotated with their respective identifier.

The result of the normalisation is used in parallel to build the Platform Literature evidence covered in a different [section](evidence.md#europe-pmc).

#### Literature-based similar entities

In order to define a strategy to find similar entities based on literature, the resulting matched entities are later used to train a Word2Vec model; the hyper-parameter settings used to train the model are taken following the suggestion from the benchmark conducted by Benjamin et al. (2020).&#x20;

By using this model, the user can query what are other entities similar to the one selected, based on all the corpus of literature. Similarly, several entities can be selected and the product of their vectors can propose additional entities similar to all the selected entities.&#x20;

The Bibliography section uses this algorithm to navigate the universe of publications. As a user keeps selecting entities, the universe is narrowed to show the intersection of all the publications that mention all of the selected entities.&#x20;

## Publications

Ferguson C, Araújo D, Faulk L, Gou Y, Hamelers A, Huang Z, Ide-Smith M, Levchenko M, Marinos N, Nambiar R, Nassar M, Parkin M, Pi X, Rahman F, Rogers F, Roochun Y, Saha S, Selim M, Shafique Z, Sharma S, Stephenson D, Talo' F, Thouvenin A, Tirunagari S, Vartak V, Venkatesan A, Yang X, McEntyre J. **Europe PMC in 2020**. Nucleic Acids Res. 2021 Jan 8;49(D1):D1507-D1514. doi: [10.1093/nar/gkaa994](https://doi.org/10.1093/nar/gkaa994). PMID: [33180112](https://pubmed.ncbi.nlm.nih.gov/33180112/); PMCID: [PMC7778976](https://europepmc.org/article/PMC/PMC7778976).

Benjamin P. Chamberlain, Emanuele Rossi, Dan Shiebler, Suvash Sedhain, and Michael M. Bronstein. 2020. Tuning Word2vec for Large Scale Recommendation Systems. In Fourteenth ACM Conference on Recommender Systems (RecSys '20). Association for Computing Machinery, New York, NY, USA, 732–737. DOI:[https://doi.org/10.1145/3383313.3418486](https://doi.org/10.1145/3383313.3418486)
