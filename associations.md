# Target - disease associations

Each unique target - disease pair in the Open Targets Platform is defined as an **association**. For example, while there might be several pieces of evidence referring to CFTR and Cystic fibrosis from multiple sources, one single association contextualises all these information within the platform. Also, as multiple pieces of evidence might refer to the same or similar associations, a series of steps are required, in order to quantify their relative strength for a given association.

## Ontological selection of evidence

The most obvious type of association aggregates evidence referring to the specific target and disease. For example, when quantifying the association between inflammatory bowel disease and NOD2, evidence is sometimes collated when annotated with these two terms specifically. The Platform refers to associations described by aggregated evidence between two specific terms in our data sources as **direct associations**. By default, direct associations are displayed in the web application when listing associated diseases or phenotypes with a target of interest.

However, evidence can sometimes be informative to discriminate targets in similar diseases or phenotypes. For example, when evaluating the inflammatory bowel disease and NOD2 association, other pieces of evidence describing the relationship between Crohn's disease and NOD2 might as well be informative. To approach this problem systematically, the Platform makes use of the properties of the disease ontology (EFO), to select all evidence referring to NOD2 in the context of inflammatory bowel disease or any of its ontology descendants (including Crohn's disease). This type of associations is referred in the platform as **indirect associations**. Indirect associations are displayed in the web application when displaying all the evidence for a target- disease association or listing associated targets with a disease or phenotype of interest.

Both direct and indirect associations can be queried using the GraphQL API and fixing a target or alternatively a disease or phenotype of interest. You can also download the entire dataset of direct and indirect associations from [our data downloads page](https://platform.opentargets.org/downloads).

{% hint style="info" %}
Note: RNA expression data type evidence is not propagated in the ontology. We made this decision to prevent parent terms from having long lists of associated targets with weak RNA expression association scores.
{% endhint %}

## Association scores

Deciding what constitutes a strong association is open to interpretation. While some data sources can be more deterministic about the underlying causal evidence, others can occasionally point to targets indirectly linked to the disease. The Platform relies on a series of heuristics to maximise the transparency of the target and disease rankings.

### By data source

A single data source might capture many pieces of evidence referring to the same target and disease. Some data sources might be more stringent when it comes to defining what constitutes a single piece of evidence, whereas others might rely on the evidence score to stratify a more relaxed definition of evidence. For all cases, the Platform defines a **data source association score** by calculating the harmonic sum using the full vector of evidence scores. The resulting sum is then divided by the maximum theoretical value of the harmonic sum to provide a data source association score between 0 and 1. The higher the score the stronger the association.

![](.gitbook/assets/Scoring\_Harmonic\_Sum\_Visual.png)

### By data type

To provide a score capturing the strength of the supporting evidence at the data type level (e.g. Genetic Associations), **data type association scores** are calculated by calculating a second harmonic sum using the weighted vector of data source association scores for the data type of interest and dividing them by the maximum theoretical value. The resulting score ranges from 0 to 1.

### Overall

The **overall association scores** aim to summarise all the aggregated evidence for an association. Similar to the score by data type, overall scores are estimated by calculating a harmonic sum using the weighted vector of data source association scores for all data sources. The resulting sum is divided by the maximum theoretical value, resulting in an overall score between 0 and 1.

### Data source weights

To calculate both data type and overall association scores, evidence is weighted using a factor that aims to calibrate the relevance of each data source relative to others. The default weights used in the web application can be modified by the user in the API, to adjust to different prioritisation strategies.

| Data source                          | Weight factor |
| ------------------------------------ | ------------- |
| Europe PMC                           | 0.2           |
| Expression Atlas                     | 0.2           |
| PhenoDigm                            | 0.2           |
| PROGENy                              | 0.5           |
| SLAPenrich                           | 0.5           |
| Cancer Biomarkers                    | 0.5           |
| SysBio                               | 0.5           |
| OTAR Projects (partner preview only) | 0.5           |
| Others                               | 1             |

### Interpreting association scores

There are few important considerations regarding association scores. As described above, association scores are a heuristic based on the availability of data. While scores are useful to rank lists of targets or diseases, they should not be interpreted as a confidence score on the target - disease association. For example, under-studied diseases are unlikely to produce high-scoring targets due to the lack of available evidence. In such diseases, a relatively low scoring target might still be the top-ranked target and potentially a very interesting lead from a therapeutic standpoint.

Similarly, not all associations with available target - disease evidence should be considered as legitimate target - disease associations. Some or our data sources rely on predictions to assess the relationship between a target and a disease. Thus, they should be considered with caution and always take their relative support in consideration.

![](<.gitbook/assets/Association score (documentation image) — April 2022.png>)
