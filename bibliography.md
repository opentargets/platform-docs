---
description: >-
  Computational pipeline generating lists of publications based on similar
  entities
---

# Bibliography

## Overview

The Platform Bibliography tool aims to provide context on the scientific background available in the literature regarding the target, disease or phenotype or drug entities of interest. The Platform aims to provide not only what publications have referenced the entities of interest, but also what other entities frequently occur in the literature in conjunction with the entities of interest. Open Targets has developed in collaboration with Europe PMC a pipeline that tries to maximise the literature information extraction by using a combination of Natural Entity Recognition, ontological normalisation and data analysis.

On our entity annotation pages, users also have the option of filtering the bibliography data to a specific timeframe.

## Data sources

#### Europe PMC

Europe PMC — [https://europepmc.org](https://europepmc.org/About) — is an open science database that facilitates access to a comprehensive collection of life science publications, preprints, and patents. Europe PMC provides researchers with freely available data available through their website, APIs, and bulk downloads.

In conjunction with the Europe PMC corpus, all the information required to build the Platform entities is required in order to establish a dictionary of terms and synonyms associated with each entity.

## Computational pipeline and datasets

#### Natural entity recognition (NER)

A machine learning model trained using BioBERT and a combination of curated datasets is applied on the Europe PMC corpus formed by abstracts and full-text articles. The model tags every gene-protein (GP), disease (DS) or drug (DR) entity in every publication. The resulting set provides some metadata on the publications, the sections where the matches are found and the sentences, where more than one type of entity co-occur.

#### Entity normalisation

In order to ground the tagged text to the Platform entities, a dictionary-based approach is applied to the tagged entities by applying a series of standard Natural Language Processing tools (e.g. stemming, stop-words, etc.). As a result, a fraction of the tagged sentences are grounded to the Platform entities and annotated with their respective identifier.

The result of the normalisation is used in parallel to build the Platform Literature evidence covered in a different [section](evidence.md#europe-pmc).

#### Literature-based similar entities

In order to define a strategy to find similar entities based on literature, the resulting matched entities are later used to train a Word2Vec model; the hyper-parameter settings used to train the model are taken following the suggestion from the benchmark conducted by Benjamin et al. (2020).

By using this model, the user can query what are other entities similar to the one selected, based on all the corpus of literature. Similarly, several entities can be selected and the product of their vectors can propose additional entities similar to all the selected entities.

The Bibliography section uses this algorithm to navigate the universe of publications. As a user keeps selecting entities, the universe is narrowed to show the intersection of all the publications that mention all of the selected entities.

## OpenAI literature summarisation tool

For data features that link to publications, the Platform now provides the option for users to ask for a natural language summary of the target-disease evidence presented in the publication (when the full-text article is available and free to re-use).

Using LangChain, we prompt OpenAI’s GPT-4o mini model to summarise relevant portions of the text which we then ask it to summarise with the following prompt: “Can you provide a concise summary about the relationship between \[target] and \[disease] according to this study?“. The resulting text is presented to the user (see screenshots with example).

<figure><img src=".gitbook/assets/Screenshot 2024-10-13 at 18.43.05.png" alt=""><figcaption><p>Arrows annotate source of publication evidence and prompt button for the feature</p></figcaption></figure>

<figure><img src=".gitbook/assets/Screenshot 2024-10-13 at 18.45.24.png" alt=""><figcaption><p>Arrow shows prompted OpenAi summary</p></figcaption></figure>

We hope this feature will help the user better understand the available bibliography evidence, and it may actually highlight cases in which the publication does not in fact provide evidence for the target-disease relationship in question.

You can find details on the OpenAI [terms of use](https://openai.com/policies/terms-of-use) here.

## Publications

Rosonovski S, Levchenko M, Bhatnagar R, et al. Europe PMC in 2023. Nucleic Acids Research. 2024 Jan;52(D1):D1668-D1676. DOI: 10.1093/nar/gkad1085. PMID: [37994696](https://pubmed.ncbi.nlm.nih.gov/37994696/); PMCID: [PMC10767826](https://europepmc.org/article/MED/37994696).

Benjamin P. Chamberlain, Emanuele Rossi, Dan Shiebler, Suvash Sedhain, and Michael M. Bronstein. 2020. Tuning Word2vec for Large Scale Recommendation Systems. In Fourteenth ACM Conference on Recommender Systems (RecSys '20). Association for Computing Machinery, New York, NY, USA, 732–737. DOI:[https://doi.org/10.1145/3383313.3418486](https://doi.org/10.1145/3383313.3418486)
