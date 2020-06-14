# interactias
## To extract and study species interation data for invasive species impact assessment

## Methods
* The script takes a single species as input and searches for all primary interacting species on GloBI (https://www.globalbioticinteractions.org/).
* Then it goes back to GloBI to get all the interacting species of those primary interacting species.
* The script then checks to see if all those species exist on GBIF (https://www.gbif.org/) and it outputs a list of missing species.
* We then use a occurrence cube of species, 1km grid square and year to evaluate the 1km occupancy of each species in the country of interest.
* Any interactions that can't occur in the country are removed.
* Visualizations are then created to display the result in a way that allows exploration of the network.

* These outputs can then be provided to expert risk assessors who can use them the evaluate what interactions might occur between an alien species and resident organisms, but also evaluate, to some extent, the impact of the interaction with reference to the occupancy.

![Diagram of the Interactias workflow](./images/interactias.png)

![An example created for *Rousettus aegyptiacus* and its interacting species were it to occur in Belgium]
(./images/Rousettusaegyptiacus.png)

## pygbif needs to be installed

e.g. Using the Anaconda Prompt run `pip install pygbif`
