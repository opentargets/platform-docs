# Data and code access

To support systematic identification and prioritisation of drug targets, we are committed to making our data open and available in a variety of formats to support academic research purposes and commercial activities. For more information, see our [Licence documentation](../licence/).

For queries about a **single entity or target-disease association**, we recommend that you use:

* Our intuitive [web interface](../web-interface.md) with data tables and data visualisations that can be downloaded/exported in multiple formats, including TSV and JSON
* Our robust [GraphQL API](graphql-api.md) with endpoints that can be accessed with the programming language of your choice and an [interactive playground](http://api.platform.opentargets.org/api/v4/graphql/browser) where you can try out sample queries

For more **complex, systematic queries**, we recommend that you use:

* Our comprehensive set of [data downloads](https://platform.opentargets.org/downloads) available via [FTP](https://ftp.ebi.ac.uk/pub/databases/opentargets/platform/), [Google Cloud](https://console.cloud.google.com/marketplace/product/bigquery-public-data/open-targets-platform?project=open-targets-genetics\&inv=1\&invt=Abwwaw), [Microsoft Azure Open Datasets](https://learn.microsoft.com/en-us/azure/open-datasets/dataset-open-targets) and [AWS Open Dataset ](s3://open-targets-public-data-releases).
* Our [Google BigQuery](google-bigquery.md) instance that supports SQL-like queries and allows you to export data to your own Google Cloud Storage bucket. This data is available as a [BigQuery Public Dataset](https://cloud.google.com/bigquery/public-data).

If you use our data in your research or commercial product, please [cite our latest publication](../citation.md).

### New export functionality

We have designed and developed a new export functionality for the Associations On the Fly/Target Prioritisation pages, allowing users to download:

* Entire dataset view (default status)
* Customised dataset view including custom controls changes, subset of data types (aggregations) and/or data from pinned targets only
* TSV and JSON formats
