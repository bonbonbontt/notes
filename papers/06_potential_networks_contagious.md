## Potential Networks, Contagious Communities and Understanding Social Network Structure (www 2013)
---
### Overview
This paper provides evidence that *online* social network datasets are not
representative of the structural properties in *real* social networks. It provides
an alternative explanation of typical structural properties observed in network datasets
and proposes a network model that uses cascades to construct online social networks
from underlying real social networks (potential networks).

### Motivation
- OSN data is not representative of social structures in a broader context.
- Contagious communities, such as OSNs, grow by adding new members. New members
get "infected" by forming social ties. It is difficult to know if structure of
contagious communities generalize. For example, contagious communities formed
using the proposed method from an underlying Watts-Strogatz model can have a power
law distribution.
- Consequently, modeling edge formation in OSNs and the like is not entirely
representative of friendships/citations/edges in the underlying network.
- These results provide a natural framework for developing generative models for contagious communities;
start with a model for an underlying social network and model a contagion spreading over it
- In a model where social networks are not created ex nihilo, but from existing social structures,
contagious networks provide a sort of sampling technique for learning the underlying structure.
- To use this data to make assertions about social questions or model social phenomena,
we need to know that the data generalizes past the digital world.

### Models
- Watts Strogatz and Planted Community model are used as underlying social network models.
These models do not exhibit real-world network properties such as heavy tailed degree distribution.
- 4 models of transmission are used to obtain subgraphs/contagious communities from graphs generated
from the above models. The subgraphs exhibit real-world network structure.
    - random transmission induced graph - incrementally build subgraph by random
    sampling edges going from S to \hat{S}. Stop once m edges are sampled.
    - extensions: random transmission where with probability beta, each edge in the induced
    graph is added and with probability alpha, edge edge from S to S complement is added at
    every timestep. random transmission w. multiple seeds. random transmission w. triadic closure.
- these transmission models generate graphs w. heavy tail degree distribtion, shrinking diameters,
edge densification, network community profile, even though the underlying graphs do not have these
properties.
- section 4 provides a proof sketch to show that applying random transmission to planted clique model
yields a subgraph with power law distribution and intuition to show that forest fire is similar to
random transmission with triadic closure.
- Theory assumes that the underlying social network structure has high clustering. Without
high clustering, sampling mechanism cannot generate graphs that are significantly different from
the underlying graph. This is why running transmission models on Erdos-Renyi graphs and preferential attachment graphs
does not yield subgraphs with realistic structure.

### Implications
1. new kind of network growth models to obtain contagious communities
    - step 1: model underlying social network structure through social phenomena
    - step 2: model transmission model to obtain "contagious" networks that exhibit strucural properties
2. contagious networks and social networks require different models
    - Indeed, we should not a priori expect all properties to be universal, and thus we should not a priori expect one generative model
    - Using data from contagious social networks may mislead us if we try to directly use it to understand social networks.
3. opportunities
    - In a model where social networks are not created ex nihilo, but from existing social structures, contagious networks provide a sort of sampling technique for learning the underlying social network.
    - given underlying graph G, what properties can and cannot be recovered from sampling?
    - algorithms to "reverse engineer" observed contagious networks and obtain real network