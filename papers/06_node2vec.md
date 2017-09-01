# Node2Vec

## Summary
- framework that uses skipgram model to learn continous feature representations (independent of ML task) for nodes in networks by maximizing the probability of preserving nodes' neighborhoods
- neighborhood is sampled using a sampling strategy that uses a biased random walk parameterized by in-out parameter to control locality and return parameter to encourage exploration
- hand-engineered features are task-specific and have limitations, current unsupervised learning in networks based on dimensionality reduction rely on eigendecomposition, which is not scalable; neighborhood preserving frameworks such as deepwalk and line have rigid definitions of neighborhood (1hop and 2hop) that limit exploration
- nodes characterized by structural role (degree, weak-strong tie) and homophily-based role (community)
- feature representations of edges can be defined as a function of the feature representations of its endpoints
- unlike text, no rigid sequence of nodes in the network. Need sampling strategy to sample nodes from neighborhood and turn network into ordered sequence of nodes. 

## Feature learning
- maximizes probability of observing network neighborhood of node u, N_S(u|f(u)), sampled using strategy S as a function of its feature representation
- assumes conditional independence of neighborhood nodes; ignores edge orientation - P(u|f(v)) = P(v|f(u)), softmax
- node u's neighborhood generated, size of set constrained, repeated multiple times
- BFS and DFS are extreme search strategies, BFS focuses on local neighborhood and DFS samples nodes at increasing distances. BFS reflects micro-neighborhood that helps in inferring local neighborhoods. DFS reflects macro-neighborhood that helps in inferring communities 
- biased random walk with parameters p, q used to sample nodes from neighborhood. Probability of sampling same node is 1/p (unnormalized). Probability of sampling node in 1-hop neighood is 1 and probability of sampling nodes at distance 2 is 1/q. low p -> micro-neighorhood, low q (rel. to p) -> DFS-like macro-neighborhood
- skipgram model used with sampled neighborhoods to learn feature representations of nodes. Different functions (avg, weighted Lp, Hadamard) using to gen. edge feature reprsentations (for link prediction)

## Experiments
- different random walk sampling parameters yield different representations. low q random walk reveals communities, low p random walk reveals structural roles (core, bridge etc)
- node label classification and link prediction. feature representations used; perfomance compared to deepwalk, spectral clustering, line
	- DeepWalk [24]: This approach learns d-dimensional feature representations by simulating uniform random walks. The sampling strategy in DeepWalk can be seen as a special case of node2vec with p = 1 and q = 1.
	- LINE [28]: This approach learns d-dimensional feature rep- resentations in two separate phases. In the first phase, it learns d/2 dimensions by BFS-style simulations over imme- diate neighbors of nodes. In the second phase, it learns the next d/2 dimensions by sampling nodes strictly at a 2-hop distance from the source nodes.
- multilabel classification (semi supervised)
	- learn feature vectors for all nodes
	- use subset of vectors w. labels to train classifier (one-vs-rest logreg with L2)
	- predict labels for remaining nodes
	- node2vec outperforms rest; evaluation: micro and macro F1; reason-flexible sampling strategy
	- perturbation analysis used to evaluate how model deals with inaccurate data, is model robust? perturb network by adding edges between random ndoes and removing existing edges
- link prediction
	- remove existing edges; use feature represetnations + classifier to predict probability of link between 2 random edges
	- evaluated against heuristic scores (hand-engineered) features such as common neighbors, jaccard, adamic-adar and PA + line, deepwalk


