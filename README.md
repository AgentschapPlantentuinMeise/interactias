# Interactias
## A Jupyter notebook to extract and study species interation data for alien species

## Methods
* The script takes a single species as input and searches for all primary interacting species on GloBI (https://www.globalbioticinteractions.org/).
* Then it goes back to GloBI to get all the interacting species of those primary interacting species.
* The script then checks to see if all those species exist on GBIF (https://www.gbif.org/) and it outputs a list of missing species.
* We then use a occurrence cube of species, 1km grid square and year to evaluate the 1km occupancy of each species in the country of interest.
* Any interactions that can't occur in the country are removed.
* Visualizations are then created to display the result in a way that allows exploration of the network.

* These outputs can then be provided to expert risk assessors who can use them the evaluate what interactions might occur between an alien species and resident organisms, but also evaluate, to some extent, the impact of the interaction with reference to the occupancy.

![Diagram of the Interactias workflow](./images/interactias.png)
Figure 1. A flow diagram to explain the script and the sources of the data. Steps after the Visualization are manual steps conducted with expert risk assessors.

![An example created for *Rousettus aegyptiacus* and its interacting species were it to occur in Belgium](./images/Rousettusaegyptiacus.png)

Figure 2. An example of a network create by this notebook and then visualized in Gephi (https://gephi.org/). The target species was the Egyptian fruit bat (*Rousettus aegyptiacus* (Geoffroy, 1810)) and the target country was Belgium. Egyptian fruit bat does not naturally occur in Belgium, but should they escape from a zoo it can be seen that they are unlikely to survive. Not only are their only food plants rare in Belgium, but they have a common predator, cats (*Felis catus* L.). In this illustration the node radius is proportional to the occupancy of that species in Belgium. The colours are modularity classes of the network. Although this is rather an extreme example, it illustrates how networks can be used to inform and evidence ecological understanding.


## pygbif needs to be installed

e.g. Using the Anaconda Prompt run `pip install pygbif`
