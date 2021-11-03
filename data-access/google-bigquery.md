# Google BigQuery

To support more complex queries and advanced informatics workflows that use Google Cloud services, the Open Targets Platform data is also available via our Google BigQuery instance - [open-targets-prod](https://console.cloud.google.com/bigquery?p=open-targets-prod\&d=platform\_21\_06).

## What is Google BigQuery?

Google BigQuery is a data warehouse that enables researchers to run super-fast, asynchronous SQL queries using Google's cloud infrastructure. After running your query, you can either export into various formats or copy into a Google Cloud bucket for further downstream analyses.

## BigQuery access points

Open Targets has uploaded all of our data to Google BigQuery. You can run queries via:

* [Cloud Console](https://cloud.google.com/bigquery/docs/quickstarts/quickstart-web-ui)
* [Command line `bq` tool](https://cloud.google.com/bigquery/docs/quickstarts/quickstart-command-line)
* [Client libraries, including Python](https://cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries)

For more information on BiqQuery, please review the [BigQuery documentation](https://cloud.google.com/bigquery/docs).

## Example BigQuery SQL queries

Below is a sample query that uses our `associationByOverallDirect` dataset to return a list of targets associated with psoriasis (EFO\_0000676) and the overall association score.&#x20;

```sql
SELECT
  associations.targetId AS target_id,
  targets.approvedSymbol AS target_approved_symbol,
  associations.diseaseId AS disease_id,
  diseases.name AS disease_name,
  associations.score AS overall_association_score
FROM
  `open-targets-prod.platform.associationByOverallDirect` AS associations
JOIN
  `open-targets-prod.platform.diseases` AS diseases
ON
  associations.diseaseId = diseases.id
JOIN
  `open-targets-prod.platform.targets` AS targets
ON
  associations.targetId = targets.id
WHERE
  associations.diseaseId='EFO_0000676'
ORDER BY
  associations.score DESC
```

[Run this query in BigQuery](https://console.cloud.google.com/bigquery?sq=352646847630:6a545cddf1c1442884e80439c97cee52)

Similarly, you can use our `molecule` dataset and pass a list of drug trade names to find relevant information:

```sql
DECLARE
  my_drug_list ARRAY<STRING>;
SET
  my_drug_list = [ 'Premarin',
  'Calcium disodium versenate',
  'Keytruda',
  'Vioxx',
  'Humira' ];
SELECT
  id AS drug_id,
  name AS drug_chembl_name,
  tradeNameList.element AS drug_trade_name,
  drugType AS drug_type,
  isApproved AS drug_is_approved,
  blackBoxWarning AS drug_blackbox_warning,
  hasBeenWithdrawn AS drug_withdrawn,
FROM
  `open-targets-prod.platform.molecule`,
  UNNEST (tradeNames.list) AS tradeNameList
WHERE
  (tradeNameList.element) IN UNNEST(my_drug_list)
```

[Run this query in BigQuery](https://console.cloud.google.com/bigquery?sq=352646847630:9813cf8f3cb443ac9103e257bf9e8b97)

## Tutorials and how-to guides

For more information on how to use BigQuery to access Platform data and example queries based on actual use cases and research questions, check out the [Open Targets Community](https://community.opentargets.org).
