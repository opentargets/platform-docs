---
description: >-
  Navigate the classic Associations view in the Open Targets Platform, from
  which you can access the Evidence pages.
---

# Classic Associations view

In the classic association page, a target, disease or phenotype is fixed and the prioritised list of alternative entities is displayed. A more detailed explanation on associations is available in the [Target - Disease associations](../associations.md) section.

Please note that this view will be replaced by the [Associations on the Fly view](associations-on-the-fly.md) once the implementation is completed to meet all our users needs.

When listing associated diseases or phenotypes associated with a target of interest, only **direct associations** are displayed. Alternatively, **indirect associations**, as derived by the selection of evidence in the ontology, are displayed when the fixed entity is a disease or phenotype. This distinction is made to minimise the effect of the annotation sparsity, and it can be modified when querying using [our GraphQL API](../data-access/graphql-api.md).

The **association table** displays the overall and datatype association scores. When clicking on any row the user will be forwarded to the respective target - disease evidence page.

When the fixed entity is a target, two extra views are available in order to list the prioritised diseases:

* The **Bubbles view** provides a hierarchical representation of the prioritised diseases using encapsulated bubbles. The big grey circles represent all the Platform therapeutic areas and they contain prioritised diseases or phenotypes coloured by their overall association score. Due to the properties of EFO the same disease can belong to more than one therapeutic area. In this case bubbles are duplicated. A minimum score filter allows the user to adjust the view to show all diseases above a minimum overall association score.
* The **Graph view** displays the subset of the EFO directed acyclic graph containing associations for the target of interest. The node colour represents the association score. A minimum score filter allows the user to adjust the view to show all diseases above a minimum overall association score.

On the left-hand side of the association page, a number of **filters** are available in order to facet the displayed associations. When multiple filters from different sections are selected they are applied using an AND operator. If multiple filters within the same section are selected they are applied with an OR operator.

## Evidence page

Evidence pages aim to summarise all the available evidence for a given target-disease pair. Evidence displayed in the page includes **indirect evidence**, so the user can interrogate evidence annotated with descendants of the disease of interest.

The structure of the page follows the same structure as the profile pages including descriptions, summary widgets, and detail widgets.
