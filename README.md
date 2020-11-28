# InteractIAS
## A Jupyter notebook to extract and study species interaction data for invasive alien species

[A video explanation](https://youtu.be/LXlilo2B19I)

InteractIAS has many uses, but was specifically developed to inform invasive species risk assessment. InteractIAS takes interaction data from the Global Biotic Interactions (GloBI) database. It then combines these interactions with occupancy data derived from GBIF to create a species interaction network with nodes weighted by their area of occupancy. This allows users to evaluate if there are species that might be impacted directly or indirectly by an invasive species. By weighing the nodes by the occupancy, it allows users to evaluate whether the interaction is likely to have a major impact or not.
Interactions between species are the most important way that invasive species impact other biodiversity. Ecosystem models are not yet sophisticated enough to interpret complex interaction networks, so we must rely on expert opinion to evaluate the potential risks of a new invasive species. Yet experts in the country where the species is invasive are not likely to have expertise in a species that may come from another continent. Therefore, we need tools to support risk assessors do their job and support their conclusions.

## Example outputs
Invasive in Belgium | Possibly invasive | Native
------------ | ------------- | -------------
*[Impatiens glandulifera](https://agentschapplantentuinmeise.github.io/interactias/docs/Impatiens%20glanduliferaBelgium.html)* (Himalayan balsam) | *[Muntiacus reevesi](https://agentschapplantentuinmeise.github.io/interactias/docs/Muntiacus%20reevesiBelgium.html)* (Reeves's muntjac) | *[Fraxinus excelsior](https://agentschapplantentuinmeise.github.io/interactias/docs/Fraxinus%20excelsiorBelgium.html)* (European Ash)
*[Phytolacca americana](https://agentschapplantentuinmeise.github.io/interactias/docs/Phytolacca%20americanaBelgium.html)* (American pokeweed) | *[Wasmannia auropunctata](https://agentschapplantentuinmeise.github.io/interactias/docs/Wasmannia%20auropunctataBelgium.html)* (electric ant) | *[Vespa crabro](https://agentschapplantentuinmeise.github.io/interactias/docs/Vespa%20crabroBelgium.html)* (yellow-legged hornet) |
*[Vespa velutina](https://agentschapplantentuinmeise.github.io/interactias/docs/Vespa%20velutinaBelgium.html)* (yellow-legged hornet)  | *[Ameiurus nebulosus](https://agentschapplantentuinmeise.github.io/interactias/docs/Ameiurus%20nebulosusBelgium.html)* (brown bullhead) |
— | *[Ameiurus melas](https://agentschapplantentuinmeise.github.io/interactias/docs/Ameiurus%20melasBelgium.html)* (black bullhead) |
— | *[Boccardia proboscidea](https://agentschapplantentuinmeise.github.io/interactias/docs/Boccardia%20proboscideaBelgium.html)* |
— | *[Channa argus](https://agentschapplantentuinmeise.github.io/interactias/docs/Channa%20argusBelgium.html)* (northern snakehead) |
— | *[Gambusia affinis](https://agentschapplantentuinmeise.github.io/interactias/docs/Gambusia%20affinisBelgium.html)* (western mosquitofish) |
— | *[Procambarus clarkii](https://agentschapplantentuinmeise.github.io/interactias/docs/Procambarus%20clarkiiBelgium.html)* (Louisiana crawfish) |
— | *[Perna viridis](https://agentschapplantentuinmeise.github.io/interactias/docs/Perna%20viridisBelgium.html)* (Asian green mussel) |
— | *[Pueraria montana](https://agentschapplantentuinmeise.github.io/interactias/docs/Pueraria%20montanaBelgium.html)* (Kudzu) |
— | *[Threskiornis aethiopicus](https://agentschapplantentuinmeise.github.io/interactias/docs/Threskiornis%20aethiopicusBelgium.html)* (African sacred ibis) | 
— | *[Solenopsis richteri](https://agentschapplantentuinmeise.github.io/interactias/docs/Solenopsis%20richteriBelgium.html)* (black imported fire ant) |

In addition to an HTML output the script generates a .dot file. This format can be opened directly by the network visualization tool Gephi (https://gephi.org/).

## Methods
* The script takes a single species as input and searches for all primary interacting species in [GloBI](https://www.globalbioticinteractions.org/).
* Then it goes back to GloBI to get all the interacting species of those primary interacting species.
* The script then checks to see if all those species exist on [GBIF](https://www.gbif.org/) and it outputs a list of missing species.
* We then use an occurrence cube of species from the country of interest. This is a data cube of taxa, 1km grid squares and years from which the 1km area of occupancy is calculated.
* Any interactions that cannot occur in the country are removed.
* Visualizations are then created to display the result in a way that allows exploration of the network.

The large volume of data required for this script mean that we have used local copies of much of the data and only use the GBIF API to consult the GBIF Taxonomic Backbone (GBIF Secretariat 2019).

### GloBI Interaction Data
* The latest interactions.tsv.gz file can be downloaded from GloBI at https://www.globalbioticinteractions.org/data.html or there is a published snapshot of the file on Zenodo (http://doi.org/10.5281/zenodo.3950590).
* Interactions.tsv is then made into an SQLite (https://www.sqlite.org/) database using a script. https://github.com/AgentschapPlantentuinMeise/createGlobiDB. This database can then be recreated whenever it is felt necessary to use a newer version.

### GBIF Occurrence Data
* We use a preconstructed Belgian occurrence cube built from GBIF observations following the methodology of Oldoni et al. (2020a). Pre-made occurrence cubes for Belgium and Italy are currently available online (Oldoni et al. 2020b). http://doi.org/10.5281/zenodo.3637911
* To create your own occurrence cube instructions are available in Oldoni et al. (2020a) and all code is available on GitHub (https://github.com/trias-project/occ-cube).
* To query the occurrence cube efficiently it is imported into an SQLite (https://www.sqlite.org/) database using a script. https://github.com/AgentschapPlantentuinMeise/occcube

### pygbif needs to be installed

e.g. Using the Anaconda Prompt run `pip install pygbif`

![Diagram of the Interactias workflow](./images/interactias.png)
Figure 1. A flow diagram to explain the script and the sources of the data. Steps after the visualization are manual steps conducted with expert risk assessors.

![An example created for *Rousettus aegyptiacus* and its interacting species were it to occur in Belgium](./images/Rousettusaegyptiacus.png)

Figure 2. An example of a network created by this notebook and then visualized in [Gephi](https://gephi.org/). The target species was the Egyptian fruit bat (*Rousettus aegyptiacus* (Geoffroy, 1810)) and the target country was Belgium. Egyptian fruit bat does not naturally occur in Belgium, but should they escape from a zoo it can be seen that they are unlikely to survive. Not only are their only food plants rare in Belgium, but they have a common predator, cats (*Felis catus* L.). In this illustration the node radius is proportional to the occupancy of that species in Belgium. The colours are modularity classes of the network. Although this is rather an extreme example, it illustrates how networks can be used to inform and evidence ecological understanding.

## Other potential applications
* Comparing networks of current ecosystems versus those under future climate scenarios
* Comparing networks with or without keystone species
* Evaluating the impact of pesticide or herbicide usage
* Understanding the biotic pressures on rare and endangered species

## Improvements and adaptions
* The script could be adapted to size the nodes based on occupancy cooccurence.
* Users can edit the parameters of the script to omit interactions they are not interested in (e.g. visitsFlowersOf), or non-specific interactions (e.g. interactsWith).
* Pre-generated data cubes for all countries would streamline setting up of the notebook for other countries.
* The notebook only works at the species level, but can be easily adapted to create higher taxon networks. These can be a useful simplification of some complex networks.
* Running in batches to create networks for a list of species.
* Allowing the entry of more than one species to examine if and where their networks join.
* ...

## Adding additional interactions
GloBI is an enormous database of species interactions, but there are many missing (Cains et al. 2017). If you have additional interactions to add to GloBI you can do so editing a simple tab-delimited text file in a GitHub repository. Instructions are here https://github.com/globalbioticinteractions/template-dataset

Using this template, I have set up a repository specifically to collect interaction data for species on the List of Invasive Alien Species of Union concern (https://ec.europa.eu/environment/nature/invasivealien/list/index_en.htm).
This repository can be found here... https://github.com/trias-project/eu-species-of-concern-interactions
Anyone can push additions to this repository or raise issues with citations of publications that describe the interaction.


## References
* Cains, Mariana, Altimir, Nuria, Anand, Srini, Liao, William, & Shiverick, Sean. (2017). IVMOOC 2017 - Gap Analysis of GloBI: Identifying Research and Data Sharing Opportunities for Species Interactions. Zenodo. [https://doi.org/10.1101/2020.03.23.983601](https://doi.org/10.5281/zenodo.814978)
GBIF Secretariat (2019). GBIF Backbone Taxonomy. Checklist dataset https://doi.org/10.15468/39omei accessed via GBIF.org on 2020-07-25.
* Oldoni, D., Groom, Q., Adriaens, T., Davis, A.J.S., Reyserhove, L., Strubbe, D., Vanderhoeven, S. & Desmet, P. (2020a). Occurrence cubes: a new paradigm for aggregating species occurrence data. BioRxiv. 2020.03.23.983601; doi: [https://doi.org/10.1101/2020.03.23.983601](https://doi.org/10.1101/2020.03.23.983601)
* Oldoni, D., Groom, Q., Adriaens, T., Davis, A.J.S., Reyserhove, L., Strubbe, D., Vanderhoeven, S. & Desmet, P. (2020b). Occurrence cubes at species level for European countries (Version 20200205) [Data set]. Zenodo. [http://doi.org/10.5281/zenodo.3637911](http://doi.org/10.5281/zenodo.3637911)
* Poelen, J.H., Simons, J.D. & Mungall, C.J. (2014). Global Biotic Interactions: An open infrastructure to share and analyze species-interaction datasets. Ecological Informatics. [https://doi.org/10.1016/j.ecoinf.2014.08.005](https://doi.org/10.1016/j.ecoinf.2014.08.005).

