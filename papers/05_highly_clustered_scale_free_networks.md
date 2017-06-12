
## Highly clustered scale-free networks
<hr>

paper: https://arxiv.org/abs/cond-mat/0107606 (2008)

### Overview
* proposes a growth model based on finite memory of the existing nodes; finite memory effect crucial for a correct description of growing network dynamics
* As networks grow, old nodes can become inactive (social networks) or outdated (citation networks), so probability of receiving links plummets. Whether a paper is cited or not depends on the collective memory containing the popularity of the paper. Empirical evidence: scientific citations
* proposed model accounts for negative correlation between age of node and attachment rate, in addition to power law + preferential attachment. Generated networks have higher clustering too.

### BA model limitation
* BA model generate scale-free networks via preferential attachment. Only preferential attachment also leads to rich-get-richer effect (positive age-attachment correlation). However, empirical data suggests rate of acquiring links decreases after a while. BA model doesn't account for clustering in networks
* Real word networks have negative age-attachment correlation, are scale-free and have high clustering

### Growth + Deactivation model
* nodes can be active or inactive. New nodes are always active first. Once inactive, nodes do not receive in-links. Model assumes rate of deactivation of node is proportion to its indegree.
* deactivation probability P is proportional to 1/(k+a) where k is the indegree and a is the bias parameter. At any given time in the network, exactly m nodes are active. 
* Model
    * Initially, model has m nodes completely connected
    * add new active node i and form links to all m active nodes
    * deactivate one node based on probability P(k) \propto 1/(a+k)
* degree distribution of active nodes and all nodes is power law, and has asymptotically high clustering; clustering is a function of number of active nodes and bias parameter in deactivation probability.
* since nodes with higher indegree are less likely to be deactivated, the probability that new node links to node with degree k is proportional to k. * * Deactivation probability leads to linear preferential attachment.
* Captures negative correlation between node age and attachment probability by deactivating nodes eventually

### Pros and Cons
* Model distributions have closed form solutions, incorporates finite memory to fix age-attachment correlation, networks are scale free and have high clustering. Possible way to model limited information/memory of individuals joining the network.
* Model assumes node can only link to active nodes. This may not be realistic for individuals. Individuals that have access to finite number of nodes can use those nodes to make decisions to link other unseen nodes.