# Getting started

Identifying evidence implicating drug targets with diseases or phenotypes constitutes one of the pivotal challenges of the Open Targets Platform. Several steps are required to aggregate, integrate, validate, and score the collected information, in order to contextualise and weight the underlying evidence. The Platform provides a framework to allow the interactive or programmatic interrogation of target-disease evidence.

### Data model

The Open Targets data model focuses on five main entities:

* [Target](target/): understood as any candidate drug binding molecule
* [Disease or Phenotype](disease-or-phenotype/): including any disease indications, phenotypes, measurements, biological processes and other relevant traits.
* [Variant](variant.md): DNA variation that has been associated with a disease, trait, or phenotype
* [Study](study.md): source of evidence linking genetic variants to traits, diseases, and molecular phenotypes.
* [Drug](drug/): molecules that can act as medicinal products.

### Entity annotation

These entities are annotated with a variety of public data sources, as well as information about the relationships between them. A more detailed description of the annotations is provided throughout the documentation. Some examples are:

* [Target tractability assessment](target/tractability.md)
* [Target safety](target/safety.md)
* [Baseline expression](target/baseline-expression.md)
* [Molecular interactions](target/molecular-interactions.md)
* [Clinical signs and symptoms](disease-or-phenotype/clinical-signs-and-symptoms.md)
* [Pharmacovigilance](drug/pharmacovigilance.md)
* [Bibliography](bibliography.md)
* [GWAS & functional genomics](gentropy/)

### Evidence generation and association scoring

A pivotal component of the Platform is the integration of potentially causal evidence linking targets and diseases. The definition of the Platform evidence as well as expanded documentation on each of the data sources are available in the [Target - disease evidence](evidence.md) section.

In order to contextualise the information, all evidence referring to unique target-disease pairs are aggregated in the form of associations. Expanded documentation on how associations are built and scored is available in the [Target - disease associations](associations.md) section.

### Applications and data access

To start addressing therapeutic hypotheses users can find alternative ways to interface with the data:

* [Web interface](web-interface.md) at [platform.opentargets.org](http://platform.opentargets.org). The Platform web application provides a user interface to navigate data relevant for building therapeutic hypotheses. Starting from the home page search box, users can navigate to entity pages, associations pages or evidence pages.
* [Data access](data-access/). More complex hypotheses might require advance interfaces or programmatic access. The Platform aims to deliver a number of alternative ways to access data to support the most intensive queries.

More details about the open source codebase and development can be found in the [Platform infrastructure](data-access/platform-infrastructure.md) section.

## Training materials

### Online tutorial

Please note we are in the process of updating our training content following the most recent updates (25.03).

{% embed url="https://www.ebi.ac.uk/training/online/courses/open-targets-quick-tour/" %}

### Webinar

{% embed url="https://www.youtube.com/watch?v=VZQql6CnbSE" %}
