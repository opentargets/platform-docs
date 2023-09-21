# Getting started

Identifying evidence implicating drug targets with diseases or phenotypes constitutes one of the pivotal challenges of the Open Targets Platform. Several steps are required to aggregate, integrate, validate, and score the collected information, in order to contextualise and weight the underlying evidence. The Platform provides a framework to allow the interactive or programmatic interrogation of target-disease evidence.

## Platform overview

<figure><img src=".gitbook/assets/Figure 1 - Finalised.jpg" alt=""><figcaption><p>Abbreviations: D = disease/phenotype; Dr = drug; EFO = Experimental Factor Ontology; T = target</p></figcaption></figure>

### (A) Data model

The Open Targets data model focuses on three main entities:

* [Target](target/) understood as any candidate drug binding molecule
* [Disease or Phenotype](disease-or-phenotype/) including any disease indications, phenotypes, measurements, biological processes and other relevant traits.
* [Drug](drug/) molecules that can act as medicinal products.

### (B) Entity annotation

These entities are annotated with a variety of public data sources, as well as more information about the relationships between them. A more detailed description of the annotations is provided throughout the documentation. Some examples are:

* [Target tractability assessment](target/tractability.md)
* [Target safety](target/safety.md)
* [Baseline expression](target/baseline-expression.md)
* [Molecular interactions](target/molecular-interactions.md)
* [Clinical signs and symptoms](disease-or-phenotype/clinical-signs-and-symptoms.md)
* [Pharmacovigilance](drug/pharmacovigilance.md)
* [Bibliography](bibliography.md)

### (C) Evidence generation and association scoring

A pivotal component of the Platform is the integration of potentially causal evidence linking targets and diseases. The definition of the Platform evidence as well as expanded documentation on each of the data sources are available in the [Target - disease evidence](evidence.md) section.

In order to contextualise the information, all the pieces of evidence referring to unique target - disease pairs are aggregated in the form of associations. Expanded documentation on how associations are built and scored is available in the [Target - disease associations](associations.md) section.

### (D) Applications and data access

To start addressing therapeutic hypotheses users can find alternative ways to interface with the data:

* [Web interface](web-interface.md) at [platform.opentargets.org](http://platform.opentargets.org). The platform web application provides a UI to answer and wide range of therapeutic hypothesis. Starting from the home page search box, users can navigate to entity pages, associations page or evidence page to answer a wide range of therapeutic hypothesis.
* [Data access](data-access/). More complex hypothesis might require advance interfaces or programmatic access. The Platform aims to deliver a number of alternative ways to access data to support the most intensive queries.

More details about the open source codebase and development can be found in the [Platform infrastructure](infrastructure.md) section.

## Training materials

### Online tutorial

[https://www.ebi.ac.uk/training/online/courses/open-targets-quick-tour/](https://www.ebi.ac.uk/training/online/courses/open-targets-quick-tour/)

### Webinar

{% embed url="https://youtu.be/Wd2i2mQN3XM%0Ahttps://youtu.be/Wd2i2mQN3XM" %}
https://youtu.be/Wd2i2mQN3XM
{% endembed %}
