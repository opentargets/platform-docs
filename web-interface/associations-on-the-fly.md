---
description: Learn about the new associations view released in 23.09.
---

# Associations on the Fly

“[Associations on the fly](https://platform.opentargets.org/disease/EFO\_0005774/associations)” is a revamp the Open Targets Platform association page with new facets and additional built-in functionalities. This view will replace the [classic associations page](classic-associations-view.md) once the implementation is completed to meet all our users needs.

### Key features

* User control over the weighting of contributing evidence from each data source
* Ability to filter by data type (note: this is an OR filter)
* Rapid comparison of evidence for different associations
* Ability to 'pin' a list of targets to create a customised list

### Data source score weights

The data source weights are presented as an advanced option in the new user interface.\
They have been designed to allow users to dynamically modify the relative importance of the different data sources from the defaults set by Open Targets. The view automatically recomputes the association scores based on the new user-defined weights, giving this view its name: Associations On the Fly.

The new feature can be adjusted to modify the preset [Open Targets data sources scores](https://platform-docs.opentargets.org/associations#data-source-weights) and their effect on the global association score “on the fly”. This interaction ultimately enables a more tailored therapeutic hypothesis formulation.

### Evidence

Where evidence is available for a data source, clicking on the button will reveal the **detail widget** for that data source. Evidence displayed in the widget includes **indirect evidence**, so the user can interrogate evidence annotated with descendants of the disease of interest.

### Upload functionality

Users can now upload a custom list of targets or diseases of interest to obtain a tailored association/target prioritisation view.

The feature is accessible from the "upload" icon on the Associations on the Fly page. This gives users the option of uploading a file containing a custom list of targets or diseases. _The file should have one entity per row_. There are multiple allowed file formats for the uploaded file (.txt)\* , (.csv/.tsv/.xlsx)\*\* , (.json). An example format has also been provided for each file format in the feature.

The Platform then suggests potential matches between the entities in uploaded list and the ones in the Platform; the matches are provided through their platform entity ids. The users also have the option to select specific results that they wish to be displayed on the final view. Clicking the 'Pin hits' tab prompts the "Associations on the Fly" page to build up a custom view with the entities from the uploaded list.&#x20;

Watch our video describing the feature:

{% embed url="https://www.youtube.com/watch?v=Mqvr2mwA7DM" %}

{% hint style="info" %}
_\* For .txt file format, please create your input list using a text editor._

_\*\* For .csv/.tsv/.xlsx file formats, please ensure that the file has a header called_ `id`_._
{% endhint %}

### Export functionality

We have designed and developed an export functionality for the Associations On the Fly/Target Prioritisation pages, allowing users to download:

* Entire dataset view (default status)
* Customised dataset view including custom controls changes, subset of data types (aggregations) and/or data from pinned targets only
* TSV and JSON formats

### Walkthrough of the new Associations on the Fly view

{% embed url="https://www.youtube.com/watch?v=2A9bksboAag" %}
