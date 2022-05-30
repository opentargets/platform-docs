# Download datasets

To support more complex and systematic queries, we provide all datasets as data downloads.

A list of all datasets is available in the [Platform Data Downloads](https://platform.opentargets.org/downloads) page.

All Platform **datasets** are available as a distributed collection of data. This implies that for each dataset, there will be a directory with a list of partitioned files. Currently, we produce our datasets in either Parquet or JSON format. Both of these formats allow us to expose nested information in a machine-readable way. Next we describe how to download, access and query this information in a step-by-step guide.

Archive datasets, as well as input files and other secondary products are also made available in the [FTP server](http://ftp.ebi.ac.uk/pub/databases/opentargets/platform/) and Google Cloud Platform.

## Download

Below is a walkthrough on how to download the `diseases` dataset from the `21.04` release in Parquet format using different approaches.

We recommend using **lftp** with a command line client, and when using tools like _wget_, _curl_, etc., use _https://_ rather than _ftp://_

#### Using rsync

`rsync` is a command line tool for efficiently transferring and synchronising files between a computer and an external hard drive.

```bash
rsync -rpltvz --delete rsync.ebi.ac.uk::pub/databases/opentargets/platform/21.04/output/etl/parquet/diseases .
```

#### Using wget

`wget` is a command line tool that retrieves content from web servers and widely available in Unix systems.

```bash
wget --recursive --no-parent --no-host-directories --cut-dirs 8 \
https://ftp.ebi.ac.uk/pub/databases/opentargets/platform/21.04/output/etl/parquet/diseases
```

#### Using Google Cloud Platform (paywalled after 1TB)

Users with Google Cloud Platform account can download the datasets through the Google Cloud Console or using `gsutil` command-line tool.

```bash
gsutil -m cp -r gs://open-targets-data-releases/21.04/output/etl/parquet/diseases .
```

#### Other ways to access data

If you are using a non-Linux or non-Unix machine (e.g. Windows), you can access our FTP service using an FTP client like FileZilla or the Windows `ftp` command. For more information, including tips and workarounds, see the [Community Windows `ftp` thread](https://community.opentargets.org/t/how-to-query-api-by-drug-trade-name/316/3?u=ahercules).

## Accessing and querying datasets

To read the information available in the partitioned datasets, there is no need to manipulate or concatenate files. Datasets can be read directly using the dataset path.

The next scripts provide a proof-of-concept example using the ClinVar evidence provided by the European Variation Archive. The next scripts show how to:

* Read a dataset
* Explore the schema of the dataset
* Select a subset of information (columns)
* Display the information

First of all the dataset needs to be downloaded as described in the previous section. For simplicity, only EVA evidence is downloaded, but all evidence can be downloaded at once using the same approach.

```bash
gsutil -m cp -r gs://open-targets-data-releases/21.04/output/etl/parquet/evidence/sourceId=eva .
```

The next scripts make use of Apache Spark ([PySpark](https://spark.apache.org/docs/latest/api/python/index.html) or [Sparklyr](https://spark.rstudio.com)) to read and query the dataset using modern functional programming approaches. These packages need to be installed in their respective environments.

The next query only displays 6 fields of the ClinVar evidence but there are other non-null values available. The **schema** is the best way to explore what's available and query the most relevant information. All Platform evidence share the same schema, so there will be a long list of fields that might not be informative for ClinVar but will be relevant if trying to query other data sources.

Dealing with nested information can sometimes be tedious. The Platform aims to minimise the nestiness of the data, however some level of structure is sometimes required. Spark provides a series of functions to deal with complex nested information. The scripts provide an example on how the `clinicalSignificances` array is flattened using the `explode` function.

Once loaded into Python or R, the user can decide to continue using Spark, write the output to a file or use alternative libraries to process the information (e.g. `pandas`, `tidyverse`, etc.).

{% tabs %}
{% tab title="Python" %}
```python
from pyspark import SparkConf
from pyspark.sql import SparkSession
import pyspark.sql.functions as F

# path to ClinVar (EVA) evidence dataset 
# directory stored on your local machine
evidencePath = "local directory path - e.g. /User/downloads/sourceId=eva"

# establish spark connection
spark = (
    SparkSession.builder
    .master('local[*]')
    .getOrCreate()
)

# read evidence dataset
evd = spark.read.parquet(evidencePath)

# Browse the evidence schema
evd.printSchema()

# select fields of interest
evdSelect = (evd
 .select("targetId",
         "diseaseId",
         "variantRsId",
         "studyId",
         F.explode("clinicalSignificances").alias("cs"),
         "confidence")
 )
 evdSelect.show()

# +---------------+--------------+-----------+------------+--------------------+--------------------+
# |       targetId|     diseaseId|variantRsId|     studyId|                  cs|          confidence|
# +---------------+--------------+-----------+------------+--------------------+--------------------+
# |ENSG00000153201|Orphanet_88619|rs773278648|RCV001042548|uncertain signifi...|criteria provided...|
# |ENSG00000115718|  Orphanet_745|       null|RCV001134697|uncertain signifi...|criteria provided...|
# |ENSG00000107147|    HP_0001250|rs539139475|RCV000720408|       likely benign|criteria provided...|
# |ENSG00000175426|Orphanet_71528|rs142567487|RCV000292648|uncertain signifi...|criteria provided...|
# |ENSG00000169174|   EFO_0004911|rs563024336|RCV000375546|uncertain signifi...|criteria provided...|
# |ENSG00000140521|  Orphanet_298|rs376306906|RCV000763992|uncertain signifi...|criteria provided...|
# |ENSG00000134982|   EFO_0005842| rs74627407|RCV000073743|               other|no assertion crit...|
# |ENSG00000187498| MONDO_0008289|rs146288748|RCV001111533|uncertain signifi...|criteria provided...|
# |ENSG00000116688|Orphanet_64749|rs119103265|RCV000857104|uncertain signifi...|no assertion crit...|
# |ENSG00000133812|Orphanet_99956|rs562275980|RCV000367609|uncertain signifi...|criteria provided...|
# +---------------+--------------+-----------+------------+--------------------+--------------------+
# only showing top 10 rows

# Convert to a Pandas Dataframe
evdSelect.toPandas()
```
{% endtab %}

{% tab title="R" %}
```r
library(dplyr)
library(sparklyr)
library(sparklyr.nested)

## path to ClinVar (EVA) evidence dataset 
## directory stored on your local machine
evidencePath <- "local directory path - e.g. /User/downloads/sourceId=eva"

## establish connection
sc <- spark_connect(master = "local")

## read evidence dataset
evd <- spark_read_parquet(sc,
                          path = evidencePath)
## Browse the evidence schema
columns <- evd %>%
  sdf_schema() %>%
  lapply(function(x) do.call(tibble, x)) %>%
  bind_rows()

## select fields of interest
evdSelect <- evd %>%
  select(targetId,
         diseaseId,
         variantRsId,
         studyId,
         clinicalSignificances,
         confidence) %>%
  sdf_explode(clinicalSignificances)

##  # Source: spark<?> [?? x 6]
##    targetId   diseaseId   variantRsId studyId  clinicalSignific… confidence     
##    <chr>      <chr>       <chr>       <chr>    <chr>             <chr>          
##  1 ENSG00000… Orphanet_8… rs773278648 RCV0010… uncertain signif… criteria provi…
##  2 ENSG00000… Orphanet_7… NA          RCV0011… uncertain signif… criteria provi…
##  3 ENSG00000… HP_0001250  rs539139475 RCV0007… likely benign     criteria provi…
##  4 ENSG00000… Orphanet_7… rs142567487 RCV0002… uncertain signif… criteria provi…
##  5 ENSG00000… EFO_0004911 rs563024336 RCV0003… uncertain signif… criteria provi…
##  6 ENSG00000… Orphanet_2… rs376306906 RCV0007… uncertain signif… criteria provi…
##  7 ENSG00000… EFO_0005842 rs74627407  RCV0000… other             no assertion c…
##  8 ENSG00000… MONDO_0008… rs146288748 RCV0011… uncertain signif… criteria provi…
##  9 ENSG00000… Orphanet_6… rs119103265 RCV0008… uncertain signif… no assertion c…
## 10 ENSG00000… Orphanet_9… rs562275980 RCV0003… uncertain signif… criteria provi…
## # … with more rows

# Convert to a dplyr tibble
evdSelect %>%
  collect()
```
{% endtab %}
{% endtabs %}

## Tutorials and how-to guides

For more information on how to access and work with [our data downloads](https://platform.opentargets.org/downloads/data) and example scripts based on actual use cases and research questions, check out the [Open Targets Community](http://community.opentargets.org).
