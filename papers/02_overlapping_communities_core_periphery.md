#### Overview
This paper proposes a new method to detect overlapping and hierarchical communities by challenging the assumption of relatively low edge density in regions where communities overlap and explains how different kinds of communities lead to the core-periphery network structure.

#### Communities and AGM
* Objective is to identify functional role-specific communities based on common structural characteristics
* Probability that 2 nodes are connected is directly proportional to number of shared functional (ground-truth) communities they're in. This challenges the assumption of common community detection methods such as mixed membership SBMs that communities are dense pockets and that edge probability is inversely proportional to the number of shared communities
* Community-affiliation graph model (AGM) is used to decompose networks into overlapping communities and reason that dense network cores formed by these communities lead to core-periphery structure
* Challenges structural view of communities that depends on triadic closure and weak ties, as it does not account for overlaps or hierarchies. Implicitly assumes that overlapping regions will be less densely connected (weak ties). Need to redefine communities
* Redefine communities as tiles. Intuitive way of understanding overlapping communities and increased edge density in those regions & core periphery structure. Definition relies on web of group affiliations, not triadic closure and weak ties. 
* Homophily in structural definitions defined to operate in dense nonoverlapping pockets; Contradicts results that homophily depends on number of shared communities. Nodes are more similar in overlapping regions; Explains why overlapping regions have higher edge density
* AGM model first decomposes network into communities and infers parameter p, which indicates the probability that 2 nodes in the same community connect. Consequently, more chances to connect if 2 nodes in multiple shared communities
  * Significant improvement of detecting ground truth communities, especially if communities overlap because other models assume that overlapping regions are less densely connected

#### Core-Periphery structure
* core-periphery networks have a densely connected core and sparsely connected periphery
* overlapping communities lead to pluralistic homophily, which leads to dense core in some networks and multiple dense cores in others
* core-periphery structure
  * pluralistic homophily leads to overlapping regions that have higher edge density
  * average number of community memberships decreases with distance from network center. Nodes in center have higher edge density
  
#### HBA
* AGM model to connect nodes with multiple attributes, infer relative importance of each attribute
* Do HBA graphs have core-periphery structure? (timestamps?)
* Link number of cores to assortativity
* AGM model interpretability
* Apply AGM to patents dataset
* Analyze edge density of first K nodes

#### Paper
https://cs.stanford.edu/people/jure/pubs/communities-pieee14.pdf