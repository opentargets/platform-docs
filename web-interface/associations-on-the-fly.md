---
description: Learn about the updated associations view
---

# Associations on the Fly

“[Associations on the Fly](https://platform.opentargets.org/disease/EFO_0005774/associations)” is a revamp the Open Targets Platform association page with new facets and additional built-in functionalities. This view replaced the classic associations page.

In the Associations on the Fly page, a target or disease/phenotype is fixed and the prioritised list of alternative entities is displayed. A more detailed explanation on associations is available in the [Target-Disease associations](../associations.md) section.

### Key features

* Rapid comparison of evidence for different associations
* User control over the weighting of contributing evidence from each data source
* Ability to include and filter by specific data sources (Note: this is an OR filter)&#x20;
* Searching and applying filters by various target, disease or phenotype categories
* Ability to 'pin' a list of targets to create a customised list
* Upload a list of interested entities and export results
* Ability to propt a 'target interactors' subview

### Data source score weights

The data source weights are presented as an advanced option in the new user interface.\
They have been designed to allow users to dynamically modify the relative importance of the different data sources from the defaults set by Open Targets. The view automatically recomputes the association scores based on the new user-defined weights, giving this view its name: Associations on the Fly.

The new feature can be adjusted to modify the preset [Open Targets data sources scores](https://platform-docs.opentargets.org/associations#data-source-weights) and their effect on the global association score “on the fly”. This interaction ultimately enables a more tailored therapeutic hypothesis formulation.

### Evidence

Where evidence is available for a data source, clicking on the button will reveal the **detail widget** for that data source. Evidence displayed in the widget includes **indirect evidence**, so the user can interrogate evidence annotated with descendants of the disease or phenotype of interest.

### Filtering functionality

The Platform comes with a re-designed functionality which allows filtering on the Associations on the Fly and Target Prioritisation pages:

* **On a disease or phenotype** **page**: Users can search and apply target specific filters which filters the association and prioritisation pages by a particular target or a target category (categories details in the table below). The default is All Categories, however you can also select and view filter suggestions for a specific category from the drop down menu.&#x20;

<table><thead><tr><th width="136">Filter category</th><th width="426">Explanation</th><th>Example</th></tr></thead><tbody><tr><td>Names</td><td>Name of the target (<code>approvedName</code>)</td><td>interleukin 13, tyrosine kinase 2</td></tr><tr><td>Symbol</td><td>Target symbol (<code>approvedSymbol</code>)</td><td>IL13, TYK2 </td></tr><tr><td>ChEMBL Target Class</td><td>Class of drug target from the ChEMBL database</td><td>Enzyme, Kinase, Surface antigen</td></tr><tr><td>GO:BP</td><td>Gene Ontology: Biological Process<br>The larger processes, or ‘biological programs’ accomplished by multiple molecular activities</td><td>DNA repair, Intracellular signal transduction</td></tr><tr><td>GO:CC</td><td>Gene Ontology: Cellular Component<br>A location, relative to cellular compartments and structures, occupied by a macromolecular machine</td><td>Cytoskeleton, Clathrin complex</td></tr><tr><td>GO:MF</td><td>Gene Ontology: Molecular Function<br>Molecular-level activities performed by gene products</td><td>Oxidoreductase activity, Transporter activator activity</td></tr><tr><td>Reactome</td><td>Pathways from the Reactome database</td><td>Circadian clock, Interleukin-6 signaling</td></tr><tr><td>Subcellular Location</td><td>Subcellular location from UniProt and HPA</td><td>Cell membrane, Cytoplasm</td></tr><tr><td>Target ID (ENSG)</td><td>Ensembl gene IDs of the target, beginning with ENSG (<code>id</code>)</td><td>ENSG00000169194, ENSG00000105397</td></tr><tr><td>Tractability Antibody</td><td><a href="https://platform-docs.opentargets.org/target/tractability#antibody">Tractability assessments for a target</a> with data on an accessible epitope for antibody based therapy</td><td>UniProt loc high conf, Human Protein Atlas loc</td></tr><tr><td>Tractability Other Modalities</td><td><a href="https://platform-docs.opentargets.org/target/tractability#assessments">Tractability assessments for a target</a> with data on compound in clinical trials with a modality other than small molecule or antibody</td><td>Approved Drug</td></tr><tr><td>Tractability PROTAC</td><td><a href="https://platform-docs.opentargets.org/target/tractability#protac">Tractability assessments for a target</a> with data on using Proteolysis Targeting Chimeras (PROTACs)</td><td>UniProt Ubiquitination, Half-life Data</td></tr><tr><td>Tractability Small Molecule</td><td><a href="https://platform-docs.opentargets.org/target/tractability#small-molecule">Tractability assessments for a target</a> with data on binding site suitable for small molecule binding</td><td>Structure with Ligand, High-Quality Pocket</td></tr><tr><td>All Categories</td><td>Search and apply all of the above filters</td><td>IL13, ENSG00000105397</td></tr></tbody></table>

* **On a target page**: Users can search and apply disease or phenotype specific filters allowing them to filter the association page by a particular disease/phenotype or a disease/phenotype category \[Disease, Therapeutic Area (eg Infectious disease, Endocrine system disease)].

{% hint style="info" %}
- Whenever you select a specific category, a few suggestions from the selected category are shown by default.
- When multiple filters from different categories are selected, they are applied using an **AND** operator. When multiple filters within the same category are selected, they are applied with an **OR** operator.
{% endhint %}

Check out this tutorial video to know more about this feature:

{% embed url="https://youtu.be/-OU3ha7XPaU?si=9unxwQgGVReDUSd3" %}

### Upload functionality

Users can now upload a custom list of targets or diseases or phenotype of interest to obtain a tailored association/target prioritisation view.

The feature is accessible from the "upload" icon on the Associations on the Fly page. This gives users the option of uploading a file containing a custom list of targets or diseases or phenotype. _The file should have one entity per row_. There are multiple allowed file formats for the uploaded file (.txt)\* , (.csv/.tsv/.xlsx)\*\* , (.json). An example format has also been provided for each file format in the feature.

The Platform then suggests potential matches between the entities in uploaded list and the ones in the Platform; the matches are provided through their platform entity ids. The users also have the option to select specific results that they wish to be displayed on the final view. Clicking the 'Pin hits' tab prompts the "Associations on the Fly" page to build up a custom view with the entities from the uploaded list.&#x20;

Watch our video describing the feature:

{% embed url="https://www.youtube.com/watch?v=Mqvr2mwA7DM" %}

{% hint style="info" %}
_\* For .txt file format, please create your input list using a text editor._

_\*\* For .csv/.tsv/.xlsx file formats, please ensure that the file has a header called_ `id`_._
{% endhint %}

### Export functionality

We have designed and developed an export functionality for the Associations on the Fly/Target Prioritisation pages, allowing users to download:

* Entire dataset view (default status)
* Customised dataset view including custom controls changes, subset of data types (aggregations) and/or data from pinned targets only
* TSV and JSON formats

### Target Interactors View

This interactive view enables access to target interactions information within the main "Associations on the Fly" disease page.

The interactors subview is prompted by one of the context menu options and will contain target molecular interactions from the current Platform data feeds:

* IntAct for binary physical interactions
* Reactome for pathway-based interactions
* Signor for directional, causal interactions
* String for functional interactions

Users can select their favourite molecular interactions data source from a drop down list located on the interactions menu bar. The the paginated interactors list is then sorted by their individual target-disease associations score, while their interaction score is shown by the target name.&#x20;

Additionally, a slider on the menu bar allows changing the default interaction score cutoff for the target interactors (please note - the default cutoff interaction score is 0.42 for IntAct and 0.75 for String. No scores reported by Reactome or Signor).

### Walkthrough of the new Associations on the Fly view

{% embed url="https://www.youtube.com/watch?v=2A9bksboAag" %}

## Reference

Cruz-Castillo et al. (2025). [Associations on the Fly, a new feature aiming to facilitate exploration of the Open Targets Platform evidence](https://academic.oup.com/bioinformatics/article/41/4/btaf070/8010255). _Bioinformatics._
