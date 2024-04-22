# GraphQL API

The Open Targets Platform GraphQL — available at [http://api.platform.opentargets.org](http://api.platform.opentargets.org/api/v4/graphql/schema) — is our new API that allows for language-agnostic access to our data, along with other key benefits:

1. You can construct a query that returns only the fields that you need
2. You can build graphical queries that traverse a data graph through resolvable entities and this reduces the need for multiple queries
3. You can access the [GraphQL API playground](http://api.platform.opentargets.org/api/v4/graphql/browser) with built-in documentation and schema showing required and optional parameters
4. You can view the [schema](http://api.platform.opentargets.org/api/v4/graphql/schema) that shows the available fields for each object along with a description and data type attribute
5. You only have to use `POST` requests with a simple query string and variables object

Our GraphQL API supports queries for a single target, disease/phenotype, drug, or target-disease association. For more systematic queries (e.g. for multiple targets), please use [our data downloads](datasets.md) or [our Google BigQuery instance](google-bigquery.md).

## Available endpoints

The base URL endpoint for our new GraphQL API is:

```
https://api.platform.opentargets.org/api/v4/graphql
```

You can then access relevant data from the following endpoints:

**/target:** contains annotation information for targets including tractability assessments, mouse phenotype models, and baseline expression; also contains data on diseases and phenotypes association with the given target

**/disease:** contains annotation information for diseases and phenotypes including ontology, known drugs, and clinical signs and symptoms; also contains data on targets associated with the given disease or phenotype

**/drug:** contains annotation information for compounds and drugs including mechanisms of action, indications, and pharmacovigilance data

**/search**: contains index of all entities contained within the Platform

## Example GraphQL query

Below is an example GraphQL query for AR (ENSG00000169083) that will return Genetic Constraint and Tractability data.

```graphql
query targetInfo {
  target(ensemblId: "ENSG00000169083") {
    id
    approvedSymbol
    biotype
    geneticConstraint{
      constraintType
      exp
      obs
      score
      oe
      oeLower
      oeUpper
    }
    tractability{
      label
      modality
      value
    }
  }
}
```

[Run this query in our GraphQL API playground](https://api.platform.opentargets.org/api/v4/graphql/browser?query=query%20targetInfo%20%7B%0A%20%20target%28ensemblId%3A%20%22ENSG00000169083%22%29%20%7B%0A%20%20%20%20id%0A%20%20%20%20approvedSymbol%0A%20%20%20%20biotype%0A%20%20%20%20geneticConstraint%20%7B%0A%20%20%20%20%20%20constraintType%0A%20%20%20%20%20%20exp%0A%20%20%20%20%20%20obs%0A%20%20%20%20%20%20score%0A%20%20%20%20%20%20oe%0A%20%20%20%20%20%20oeLower%0A%20%20%20%20%20%20oeUpper%0A%20%20%20%20%7D%0A%20%20%20%20tractability%20%7B%0A%20%20%20%20%20%20label%0A%20%20%20%20%20%20modality%0A%20%20%20%20%20%20value%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A)

Using GraphQL's [query strings](https://graphql.org/learn/queries/) and [variables object](https://graphql.org/graphql-js/passing-arguments/) constructs, you can also access the data using a programming language that supports HTTP `POST` requests. While this is a valid approach, we discourage users from repeatedly querying the GraphQL API one entity at a time. Instead, our comprehensive [datasets available for download ](datasets.md)provide a simpler and more performant strategy to achieve the same result.

### Sample scripts

Below is an example script using the same AR query above, but written for Python and R:

{% tabs %}
{% tab title="Python" %}
```python
#!/usr/bin/env python3

# Import relevant libraries to make HTTP requests and parse JSON response
import requests
import json

# Set gene_id variable for AR (androgen receptor)
gene_id = "ENSG00000169083"

# Build query string to get general information about AR and genetic constraint and tractability assessments 
query_string = """
  query target($ensemblId: String!){
    target(ensemblId: $ensemblId){
      id
      approvedSymbol
      biotype
      geneticConstraint {
        constraintType
        exp
        obs
        score
        oe
        oeLower
        oeUpper
      }
      tractability {
        label
        modality
        value
      }
    }
  }
"""

# Set variables object of arguments to be passed to endpoint
variables = {"ensemblId": gene_id}

# Set base URL of GraphQL API endpoint
base_url = "https://api.platform.opentargets.org/api/v4/graphql"

# Perform POST request and check status code of response
r = requests.post(base_url, json={"query": query_string, "variables": variables})
print(r.status_code)

# Transform API response from JSON into Python dictionary and print in console
api_response = json.loads(r.text)
print(api_response)
```
{% endtab %}

{% tab title="R" %}
```r
# Install relevant library for HTTP requests
library(httr)

# Set gene_id variable for AR (androgen receptor)
gene_id <- "ENSG00000169083"

# Build query string to get general information about AR and genetic constraint and tractability assessments 
query_string = "
  query target($ensemblId: String!){
    target(ensemblId: $ensemblId){
      id
      approvedSymbol
      biotype
      geneticConstraint {
        constraintType
        exp
        obs
        score
        oe
        oeLower
        oeUpper
      }
      tractability {
        label
        modality
        value
      }
    }
  }
"

# Set base URL of GraphQL API endpoint
base_url <- "https://api.platform.opentargets.org/api/v4/graphql"

# Set variables object of arguments to be passed to endpoint
variables <- list("ensemblId" = gene_id)

# Construct POST request body object with query string and variables
post_body <- list(query = query_string, variables = variables)

# Perform POST request
r <- POST(url=base_url, body=post_body, encode='json')

# Print data to RStudio console
print(content(r)$data)
```
{% endtab %}
{% endtabs %}

## Tutorials and how-to guides

{% embed url="https://youtu.be/_sZR0VxpwqE" %}

For more information on how to use the GraphQL API and example queries based on actual use cases and research questions, check out the [Open Targets Community](https://community.opentargets.org).
