# Web interface

The web interface available at [http://platform.opentargets.org](http://platform.opentargets.org) constitutes the first point of access for most of the Platform users. The site provides a unified search box connected to a series of tools allowing users to query different therapeutic hypotheses.

When possible, users can download the displayed information, but we invite users to visit the [Data access](data-access/) section when more complex queries are under consideration.

![](<.gitbook/assets/Web interface overall journey image (documentation image).png>)

### Associations page

In the association page, a target, disease or phenotype is fixed and the prioritised list of alternative entities is displayed. A more detailed explanation on associations is available in the [Target - Disease associations](associations.md) section.

When listing associated diseases or phenotypes associated with a target of interest, only **direct associations** are displayed. Alternatively, **indirect associations**, as derived by the selection of evidence in the ontology, are displayed when the fixed entity is a disease or phenotype. This distinction is made to minimise the effect of the annotation sparsity, and it can be modified when querying using [our GraphQL API](data-access/graphql-api.md).

The **association table** displays the overall and datatype association scores. When clicking on any row the user will be forwarded to the respective target - disease evidence page.

When the fixed entity is a target, 2 extra views are available in order to list the prioritised diseases:

* The **Bubbles view** provides a hierarchical representation of the prioritised diseases using encapsulated bubbles. The big grey circles represent all the Platform therapeutic areas and they contain prioritised diseases or phenotypes coloured by their overall association score. Due to the properties of EFO the same disease can belong to more than one therapeutic area. In this case bubbles are duplicated. A minimum score filter allows the user to adjust the view to show all diseases above a minimum overall association score.
* The **Graph view** displays the subset of the EFO directed acyclic graph containing associations for the target of interest. The node colour represents the association score. A minimum score filter allows the user to adjust the view to show all diseases above a minimum overall association score.

On the left-hand side of the association page, a number of **filters** are available in order to facet the displayed associations. When multiple filters from different sections are selected they are applied using an AND operator. If multiple filters within the same section are selected they are applied with an OR operator.&#x20;

### Evidence page

Evidence pages aim to summarise all the available evidence for a given target-disease pair. Evidence displayed in the page includes **indirect evidence**, so the user can interrogate evidence annotated with descendants of the disease of interest.

The structure of the page follows the same structure as the profile pages including descriptions, summary widgets, detail widgets and navigation menu.

### Entity profile pages

Profile pages aim to describe the entity and provide relevant annotation that might become informative at different stages of the drug development process.

At the top of each profile page, we provide a description for the entity, a series of cross-references to other databases, as well as synonyms provided by some of the upstream data sources.&#x20;

Next, a list of **summary widgets** display the availability of certain category of information as well as message to provide a sense of the available information. Summary widgets in grey report the lack of information for the given category.

Further down the page, **detail widgets** provide the full extent of information available in the Platform about a particular summary widget. A description explains the nature of the displayed information, as well as the source of the data.

On the left-hand side, the **navigation menu **allows users to browse the widget of interest and re-order the widgets based on the user preference.
