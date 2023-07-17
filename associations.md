# Target - disease associations

Each unique target-disease pair in the Open Targets Platform is defined as an **association**. For example, while there might be several pieces of evidence referring to CFTR and Cystic fibrosis from multiple sources, one single association contextualises all this information within the Platform. Also, since multiple pieces of evidence might refer to the same or similar associations, the Platform undertakes a series of steps to quantify their relative strength for a given association.

## Ontological selection of evidence

The Platform associations aim to aggregate all evidence referring to the target and disease, but the complex phenotypic representation of the disease might sometimes cause different pieces of evidence to be annotated against slightly different levels of granularity of the disease.&#x20;

For example, the association between inflammatory bowel disease and NOD2 is annotated with multiple pieces of evidence referring to these two terms specifically. The Platform refers to associations described by aggregated evidence between two specific terms in our data sources as **direct associations**. By default, direct associations are displayed in the web application when listing associated diseases or phenotypes with a target of interest.

However, evidence can sometimes be informative to discriminate targets in similar diseases or phenotypes. For example, when evaluating the inflammatory bowel disease and NOD2 association, other pieces of evidence describing the relationship between Crohn's disease and NOD2 might also be informative.&#x20;

To approach this problem systematically, the Platform makes use of the properties of the disease ontology (EFO), to select all evidence referring to NOD2 in the context of inflammatory bowel disease or any of its ontology descendants (including Crohn's disease). This type of association is referred to in the platform as an **indirect association**. Indirect associations are displayed in the web application when displaying all the evidence for a target-disease association or listing associated targets with a disease or phenotype of interest.

{% hint style="info" %}
**Summary**

An association page for diseases associated with a target (e.g. [NOD2 associations page](https://platform.opentargets.org/target/ENSG00000167207/associations)) includes **direct evidence only**.

An association page for targets associated with a disease (e.g. [Inflammatory Bowel Disease associations page](https://platform.opentargets.org/disease/EFO\_0003767/associations)) includes **both direct and indirect evidence**.&#x20;

An evidence page (e.g. [NOD2 and inflammatory bowel disease](https://platform.opentargets.org/evidence/ENSG00000167207/EFO\_0003767)) displays **both direct and indirect evidence**. &#x20;
{% endhint %}

\
\
The same calculations are applied to calculate the association scores, the only difference is the evidence included in the calculation.

Both direct and indirect associations can be queried using the GraphQL API or [our data downloads page](https://platform.opentargets.org/downloads).

{% hint style="info" %}
**Note**

RNA expression data type evidence is not propagated in the ontology. We made this decision to prevent parent terms from having long lists of associated targets with weak RNA expression association scores.
{% endhint %}

## Association scores

Deciding what constitutes a strong association is open to interpretation. While some data sources can be more deterministic about the underlying causal evidence, others can occasionally point to targets indirectly linked to the disease. The Platform relies on a series of heuristics to maximise the transparency of the target and disease rankings.

### By data source

The Platform's scoring by data source aims to take into account variations in how the data sources organise their evidence.

For example, some data sources are more stringent when it comes to defining what constitutes a single piece of evidence, whereas others rely on their internal evidence score to stratify the strength of the evidence they present.&#x20;

Additionally, some data sources will capture the meaningful association in one single piece of evidence. In other data sources, the repetition of evidence increases our confidence in the association.&#x20;

The scoring by data source aims to balance all these differences and provide a consensus view on the strength of the underlying evidence for a particular source.

For all cases, the Platform defines a **data source association score** by calculating a harmonic sum using the full vector of [evidence scores](evidence.md#evidence-data-sources) as defined for each data source using the following the next steps:

1. The pieces of evidence are sorted in descending order and assigned an incremental value that indicates their position in the sorted list (the top-scoring item has a positional id of 1, the second has a positional id of 2, and so on).
2. The harmonic sum for each data source is then calculated by summing the result of dividing each evidence score by (2^positional id).

![](.gitbook/assets/Scoring\_Harmonic\_Sum\_Visual.png)

3. To ensure the result is between 0 and 1, the harmonic sum is normalised by dividing the result by the maximum theoretical harmonic sum, which is the one calculated using an infinite vector of ones. The platform derives this calculation (which approximates to 1.6) by using a vector of 1,000 ones.

{% hint style="info" %}
**Example**

To calculate the **data source association score** for a vector of evidence scored 1, 0.9 and 0.8 the Platform will follow the next logic

_Step 1: Sorting/Indexing_

```
evidence with score=1.0 -> positional id=1
evidence with score=0.9 -> positional id=2
evidence with score=0.8 -> positional id=3
```

_Step 2: Harmonic sum calculation_

```
harmonic sum score = 1.0/1^2 + 0.9/2^2 + 0.8/3^2
```

_Step 3: Scaling_

```
max. theoretical harmonic sum score = 1.0/1^2 + 1.0/2^2 + 1.0/3^2 + 1.0/4^2 + ...
normalised harmonic sum score = harmonic sum score / max. theoretical harmonic sum score
```
{% endhint %}

### By data type

The **data type association score** aims to capture the strength of the supporting evidence at the data type level (e.g. Genetic Associations). A second harmonic sum is calculated by using the vector of [data source association scores](associations.md#data-source-weights) weighted by the [data source weights](associations.md#data-source-weights).

{% hint style="warning" %}
**Association score by data type scaling**

While the harmonic sum calculation remains mostly the same for **data sources, data types** and **overall**, the scaling factor is slightly modified in the **association by** **data type** calculation.&#x20;

So that data types only featuring one data source (e.g. text mining) are not penalised, the maximum theoretical harmonic sum score is calculated based on a vector of as many ones as data sources are in the respective datatype. In this way, the scaling factor of a data type with one data source will be `1.0/1^2 = 1`, whereas a datatype with 3 data sources will be scaled by the result of calculating: `1.0/1^2 + 1/2^2 + 1/3^2 = 1.36`.
{% endhint %}

### Overall

The **overall association score** aims to summarise all the aggregated evidence for a given target-disease association. The score is derived by calculating the harmonic sum of the association score by data source weighted by the [data source weights](associations.md#data-source-weights), regardless of their data type categorisation. The algorithm to compute the scores is the same as the association by data source, resulting in a score between 0 and 1.

### Data source weights

To calculate both **data type** and **overall** association scores, evidence is weighted using a factor that aims to calibrate the relevance of each data source relative to others. The default weights used in the web application can be modified by the user in the API, to adjust to different prioritisation strategies.

| Data source                          | Weight factor |
| ------------------------------------ | ------------- |
| Europe PMC                           | 0.2           |
| Expression Atlas                     | 0.2           |
| IMPC                                 | 0.2           |
| PROGENy                              | 0.5           |
| SLAPenrich                           | 0.5           |
| Cancer Biomarkers                    | 0.5           |
| SysBio                               | 0.5           |
| OTAR Projects (partner preview only) | 0.5           |
| Others                               | 1             |

### Interpreting association scores

There are a few important considerations regarding association scores. As described above, association scores are a heuristic based on the availability of data. While scores are useful to rank lists of targets or diseases, **they should not be interpreted as a confidence score for the target-disease association**.&#x20;

For example, under-studied diseases are unlikely to produce high-scoring targets due to the lack of available evidence. In such diseases, a relatively low-scoring target might still be the top-ranked target and potentially a very interesting lead from a therapeutic standpoint.

Similarly, not all associations with available target-disease evidence should be considered legitimate target-disease associations. Some of our data sources rely on predictions to assess the relationship between a target and a disease. Thus, they should be considered with caution and always take their relative support into consideration.

![Schematic of how data source, data type, and overall associations scores are calculated in the Open Targets Platform. ](<.gitbook/assets/Association score (documentation image) — July 2023 (1).png>)
