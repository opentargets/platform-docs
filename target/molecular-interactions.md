---
description: Systematically capturing target - target interactions of different nature
---

# Molecular interactions

## **Overview**

The Molecular Interactions data aggregates and integrates interaction evidence reported in several resources to provide a systematic view on potentially relevant drug targets. Each of the integrated resources captures relationships of different nature including physical binary interactions, enzymatic reactions or functional relationships. The information here available aims to capture not only the topology of the interaction network, but also the supporting experimental evidence reported on each of the databases.

In order to maximise coverage, the network contains all reported binary relationships between gene products (proteins and RNAs). Although the main focus are interactions between human molecules, the data also includes additional interactions between human gene products and molecules encoded in the genome of infectious pathogens - viruses and bacteria.

## **Data sources**

### IntAct

IntAct - [http://www.ebi.ac.uk/intact](http://www.ebi.ac.uk/intact) - is a freely available, open source database for molecular interaction data. IntAct contains physical interactions derived from literature curation or direct user submissions.

Interactions are scored using the MI score. Benefiting from the PSI-MI controlled vocabulary, the Intact MI score provides a normalised (0 to 1) score that weights how recurrently an interaction has been reported, together with the confidence of the experimental techniques reported. Beware, a high scoring interaction can be due to high-confidence evidence, but also a social bias on studying certain proteins. Generally speaking, scores > 0.4 correspond to medium to high-confidence interactions, although some good-quality high-throughput interactions might still be scored below that threshold. More info on MI-score can be found in the [Intact documentation](https://www.ebi.ac.uk/intact/pages/faq/faq.xhtml).

Interactions are grouped by interaction detection method and interaction type. As a consequence, the same pair of interactors might be split into multiple entries if individual proteins are reported to have different biological roles.

For IntAct, please note:

* The network only contains human and selected pathogen data from IntAct
* The majority of interactions are not directional and not signed. However, there are a proportion of interactions where the biological role of the participants can be stated and directionality specified (e.g. enzymatic reactions)

### Reactome

Reactome - [https://reactome.org/](https://reactome.org) - is an open-source, open access, manually curated and peer-reviewed pathway database.

For Reactome, please note:

* Only human-human interactions are provided
* Interactions are directional and signed, with biological roles assigned to each participant if possible
* Protein interactions in Reactome are inferred from pathways and complexes based on Reactome internal [method](https://github.com/reactome/interaction-exporter/wiki/Methods).

### SIGNOR

SIGNOR, the SIGnaling Network Open Resource - [https://signor.uniroma2.it/](https://signor.uniroma2.it) - contains signaling information published in the scientific literature, which is manually-curated and stored in a structured format.

For SIGNOR, please note:

* SIGNOR only contains human data
* Interactions are directional and signed, with biological roles assigned to each participant
* The network pulls information from the SIGNOR relations file

### STRING

STRING - [https://string-db.org](https://string-db.org) - contains functionally interacting proteins. While most interactions in the other resources capture different types of physical interaction between molecules, functional interactions do not necessarily interact physically. Both, direct (physical) and indirect (functional) associations are derived from computational predictions, from knowledge-transfer between organisms, or from interactions aggregated from other (primary) databases.\
\
STRING interactions provide an overall combined\_score, as well as each of the pieces of information that compose this score. More information on STRING scoring can be found on their [documentation page](https://string-db.org/cgi/info).

## Computational pipeline and datasets

The multipartite network displayed in the Open Targets Platform is the result of post-processing the information stored in a Neo4j graph database (graphDB). The graphDB does not provide STRING information but contains ComplexPortal information on stable protein complexes as an additional data source. The information of the graphDB is then exported together with STRINGdb and mapped to the Open Targets Platform targets (Ensembl Gene IDs).

The resulting dataset as well as all intermediate files can be found in the Open Targets Platform Data Access section or the [Intact FTP](ftp://ftp.ebi.ac.uk/pub/databases/intact/various/ot\_graphdb/current/).

## Publications

When using this data please remember to acknowledge the sources:

Orchard S, Ammari M, Aranda B, Breuza L, Briganti L, Broackes-Carter F, Campbell NH, Chavali G, Chen C, del-Toro N, Duesbury M, Dumousseau M, Galeota E, Hinz U, Iannuccelli M, Jagannathan S, Jimenez R, Khadake J, Lagreid A, Licata L, Lovering RC, Meldal B, Melidoni AN, Milagros M, Peluso D, Perfetto L, Porras P, Raghunath A, Ricard-Blum S, Roechert B, Stutz A, Tognolli M, van Roey K, Cesareni G, Hermjakob H. **The MIntAct project--IntAct as a common curation platform for 11 molecular interaction databases**. Nucleic Acids Res. 2014 Jan;42(Database issue):D358-63. doi: 10.1093/nar/gkt1115. Epub 2013 Nov 13. PMID: 24234451; PMCID: PMC3965093.

Jassal B, Matthews L, Viteri G, Gong C, Lorente P, Fabregat A, Sidiropoulos K, Cook J, Gillespie M, Haw R, Loney F, May B, Milacic M, Rothfels K, Sevilla C, Shamovsky V, Shorser S, Varusai T, Weiser J, Wu G, Stein L, Hermjakob H, D'Eustachio P. **The reactome pathway knowledgebase**. Nucleic acids research. 2020 Jan;48(D1) D498-D503. doi: 10.1093/nar/gkz1031. PubMed PMID: 31691815. PubMed Central PMCID: PMC7145712.

Licata L, Lo Surdo P, Iannuccelli M, Palma A, Micarelli E, Perfetto L, Peluso D, Calderone A, Castagnoli L, Cesareni G. **SIGNOR 2.0, the SIGnaling Network Open Resource 2.0: 2019 update**. Nucleic Acids Res. 2020 Jan 8;48(D1):D504-D510. doi: 10.1093/nar/gkz949. PMID: 31665520; PMCID: PMC7145695.

Szklarczyk D, Kirsch R, Koutrouli M, Nastou K, Mehryary F, Hachilif R, Gable AL, Fang T, Doncheva NT, Pyysalo S, Bork P, Jensen LJ, von Mering C. **The STRING database in 2023: protein-protein association networks and functional enrichment analyses for any sequenced genome of interest**. Nucleic Acids Res. 2023 Jan 6;51(D1):D638-D646. doi: 10.1093/nar/gkac1000. PMID: 36370105; PMCID: PMC9825434.
