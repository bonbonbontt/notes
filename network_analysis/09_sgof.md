## Spectral Goodness of Fit
---

Link: https://arxiv.org/abs/1407.7247

### Overview
spectral goodness of fit (SGOF) to measure how well a network model explains the structure of an observed network. SGOF provides an absolute measure of fit, analogous to the standard R^2. p.2:  In particular, leveraging the features of the spectrum of the graph Laplacian, we define a new goodness of fit statistic that measures the percent improvement a network model makes over a null model in explaining the structure in the observed data.

### Motivation
Two types of network models: Likelihood-based models such as ERGMs and MAGs
& structure descriptors approach such as Watts-Strogatz, Barabasi that preserve
a set of structural properties. A limitation of structure descriptor models
is that it cannot preserve all or unknown properties. Even if the theoretical focus
of a given researcher is on a single structural issue, say, modeling geodesics,
the overall fit of the model to the whole network is still important.

### Spectral Goodness of Fit

SGOF is an absolute measure of goodness of fit of the overall network structure
that does not require the researcher to know which structural properties are
important beforehand. Limitation: Only applied to undirected networks. Spectrum
of Laplacian matrix is an ordered multiset of eigenvalues that is graph
invariant so similar structure implies similar spectrum. Number of zero-valued
eigenvalues equal number of components in the graph. The magnitude of the i^th
smallest eigenvalue equals the minimum number of ties to split the graph into
two components. The sizes of successively larger eigenvalues provide information
on successively finer divisions of the network into smaller sub-communities. The
shape of the spectrum describes how the total tie strength in a given network is
structured relative to other networks with the same total amount of tie strength
(density). **The sum of eigenvalues equals the total weight of all edges**:
sensitive to the edge density of the network. Therefore, adjacency matrix (NA) is
normalized to control for edge density by dividing each entry by the total
weight of all edges in the graph. Spectral of NA is NS. Spectral distance is
the the norm ||NS1-NS2|| where NSi is spectrum of graph i. Since  models
don't a closed form spectrum, the distance ESD is estimated by taking the average
spectral distance of simulated graphs.

To make the measure absolute, it is measured relative to the ESD of the null model
(think worst case). The final measure is 1-ESD_model/ESD_null. The SGOF measures
the amount of observed structure explained by a fitted model, expressed as a percent
improvement over a null model. SGOF allows comparison between Likelihood models
and structure descriptor models. p.17: To assess the fit of this model, one must
first find the best values for the model’s parameters, which we will do by appeal to SGOF.










