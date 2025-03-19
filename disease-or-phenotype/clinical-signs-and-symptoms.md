# Clinical signs and symptoms

## **Overview**

The Clinical Signs and Symptoms data in the Platform aims to capture other diseases or phenotypes that occur as a consequence, or in conjunction with a primary disease.

Disease–phenotype relationships are not only useful to better characterise the disease phenotypic space, but also to serve as proxies for additional causal evidence that can help prioritise new or existing targets.

In order to maximise the list of available disease–phenotype links, the Platform ingests data from the [Monarch Merged Disease Ontology](https://mondo.monarchinitiative.org) (MONDO) and the [Human Phenotype Ontology](https://hpo.jax.org) (HPO), the latter in a joint effort with [Orphanet](http://www.orpha.net).

## **Data sources**

### Monarch Merged Disease Ontology (MONDO)

The Monarch Merged Disease Ontology (MONDO) – [https://mondo.monarchinitiative.org/](https://mondo.monarchinitiative.org) – is an open-source semi-automatically constructed ontology that integrates multiple disease resources to build a single, coherent merged ontology. Originally constructed in an entirely automatic way with IDs of source databases and ontologies, manually curated cross-ontology axioms have been added and a native Mondo ID system was developed and implemented to reduce confusion with source databases and ontologies.

### Human Phenotype Ontology (HPO)

The Human Phenotype Ontology (HPO) – [https://hpo.jax.org/app/](https://hpo.jax.org/app/) – provides a standardised vocabulary of phenotypic abnormalities encountered in human disease and contains over 13,000 terms and over 156,000 annotations to hereditary diseases. HPO has been developed using medical literature, Orphanet, DECIPHER, and OMIM.

## Computational pipelines and datasets

The relationships described in MONDO and HPO are also enriched with annotations such as sex, typical age of onset or frequency of disease patients presenting the phenotype. To improve the interoperability with the rest of the Platform, diseases and phenotypes are mapped to the [Experimental Factor Ontology](https://www.ebi.ac.uk/efo/) (EFO) when possible.

Complete disease–phenotype relationship datasets are available for download on [our data downloads page](https://platform.opentargets.org/downloads).

## Publications

Köhler S, Carmody L, Vasilevsky N, Jacobsen JOB, Danis D, Gourdine JP, Gargano M, Harris NL, Matentzoglu N, McMurry JA, Osumi-Sutherland D, Cipriani V, Balhoff JP, Conlin T, Blau H, Baynam G, Palmer R, Gratian D, Dawkins H, Segal M, Jansen AC, Muaz A, Chang WH, Bergerson J, Laulederkind SJF, Yüksel Z, Beltran S, Freeman AF, Sergouniotis PI, Durkin D, Storm AL, Hanauer M, Brudno M, Bello SM, Sincan M, Rageth K, Wheeler MT, Oegema R, Lourghi H, Della Rocca MG, Thompson R, Castellanos F, Priest J, Cunningham-Rundles C, Hegde A, Lovering RC, Hajek C, Olry A, Notarangelo L, Similuk M, Zhang XA, Gómez-Andrés D, Lochmüller H, Dollfus H, Rosenzweig S, Marwaha S, Rath A, Sullivan K, Smith C, Milner JD, Leroux D, Boerkoel CF, Klion A, Carter MC, Groza T, Smedley D, Haendel MA, Mungall C, Robinson PN. **Expansion of the Human Phenotype Ontology (HPO) knowledge base and resources**. Nucleic Acids Res. 2019 Jan 8;47(D1):D1018-D1027. doi: 10.1093/nar/gky1105. PMID: [30476213](https://pubmed.ncbi.nlm.nih.gov/30476213/); PMCID: PMC6324074.

Shefchek KA, Harris NL, Gargano M, Matentzoglu N, Unni D, Brush M, Keith D, Conlin T, Vasilevsky N, Zhang XA, Balhoff JP, Babb L, Bello SM, Blau H, Bradford Y, Carbon S, Carmody L, Chan LE, Cipriani V, Cuzick A, Della Rocca M, Dunn N, Essaid S, Fey P, Grove C, Gourdine JP, Hamosh A, Harris M, Helbig I, Hoatlin M, Joachimiak M, Jupp S, Lett KB, Lewis SE, McNamara C, Pendlington ZM, Pilgrim C, Putman T, Ravanmehr V, Reese J, Riggs E, Robb S, Roncaglia P, Seager J, Segerdell E, Similuk M, Storm AL, Thaxon C, Thessen A, Jacobsen JOB, McMurry JA, Groza T, Köhler S, Smedley D, Robinson PN, Mungall CJ, Haendel MA, Munoz-Torres MC, Osumi-Sutherland D. **The Monarch Initiative in 2019: an integrative data and analytic platform connecting phenotypes to genotypes across species**. Nucleic Acids Res. 2020 Jan 8;48(D1):D704-D715. doi: 10.1093/nar/gkz997. PMID: [31701156](https://pubmed.ncbi.nlm.nih.gov/31701156/); PMCID: PMC7056945.
