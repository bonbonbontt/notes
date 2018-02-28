# Graph Convolutional Networks

## Notation/Setup
- Inputs
	- Node-level features matrix X (NxD)
	- Adjacency matrix A (NxN)
- Output
	- Node-level output features matrix Z (NxF)
- Foward propagation
	- H^(l+1) = f(H^l, A)
	- H^(0) = X, H^(L) = Z
- The specific models differ only in how f(⋅,⋅)f(⋅,⋅) is chosen and parameterized

## Intuition (Blog)

f(H^l, A) = ReLU(A H^(l) W^(l))

- H^(l): l^th layer activations
- W^(l): l^th layer weight matrix
- A: adjacency matrix

- A sums up feature vectors of neighboring nodes but not the feature vector of the main node. Fix is too add self loops:
	- f(H^l, A) = ReLU((A+I) H^(l) W^(l))

- Now, A sums of features vectors of neighboring nodes and node's feature vector. Doing so monotoncially increases the feature vector values. This is does not behave well with backprop. Scaling fix is to take average of feature vectors
	- f(H^l, A) = ReLU(inv(D')A'H^(l)W^(l))
	- so each nonzero value in inv(D')A' is 1/(d+1)


- Kipf paper: f(H^(l), A) = ReLU(inv(D^0.5)Ain(D^0.5)HW)
	- inv(D^0.5)Ain(D^0.5) is like the normalzied laplacian
	- each nonzero value in matrix is 1/sqrt(di*dj) if i and j are connected
	- if not features available, let X=I

- Multilayer forward propagation
	- H^(1) = g(inv(D')A'H^(0) W^(0)) = g(inv(D')A' X W^l)
	- H^(2) = g(inv(D')A'H^1 W^1)
	- H^1 is a nonlinear transformation of a weighted linear combination of its features and the feature vectors of the neighbors
	- H^1 features charactersize the neighborhoods of the nodes
	- H^2 is a nonlinear transformation of a weighted linear combination of the neighborhoods of all neighbors of a node
	- The 3-layer GCN now performs three propagation steps during the forward pass and effectively convolves the 3rd-order neighborhood of every node (all nodes up to 3 "hops" away

- Interpreting GCN model: Weisfeiler-Lehman algorithm with nonlinear transformation layer-wise; iteratively sharing feature vectors to "convolve" the k-th order neighborhood of every node
	- h^(l+1)_(vi) = g(sum over nbors j+i: 1/c(ij) h^l_(vj) W^l)

- Extending GCN for semi-supervised learning
	- We observe that the 3-layer GCN model manages to linearly separate the communities, given only one labeled example per class. This is a somewhat remarkable result, given that the model received no feature description of the nodes

## Paper

### Introduction
- objective: classifying nodes (such as documents) in a graph  (such as a citation network), where labels are only available for a small subset of nodes
- traditional graph based semi supervised learning loss = L0 + L_reg
	- L0 is the loss w.r.t the labelled examples
	- L_reg is graph laplacian regularization: \sum_{i,j in E} ||f(x_i)-f(x_j)||^2
	- Problem: edge does not imply similarity
- approach: encode structure using NN f(X,A), X feature matrix, training on supervised target L0 using nodes with labels, use structure to distribute gradient information to unlabelled nodes; without explicit graph regularization

### Fast approximate convolutions on graphs

setup
- self loop adj. A'=A+I
- GCN propagation: H(l+1) = g(inv(D'^0.5)A'inv(D'^0.5)H(l)W(l))
- H(l) shape (N, D) D is number of input features

spectral convolution
- signal x (N, 1), scalar for each node
- diagnol matrix g_theta = diag(theta), theta shape (N,1)
- U is eigenvector matrix of normalized laplacian L
- L = inv(D^0.5)(D-A)inv(D^0.5) = UKU^T
	- U is L's eigenmatrix
	- K is diagnol eigval matrix
- spectral convolution star(g_theta, x):
	- star(g_theta, x) = (U g_theta U^T)x
	- think of g_theta as function of eigmatrix K
	- too expensive, O(N^2) multiplication, eigendecomp. of large matrices too expensive, approximation needed
		- linear combination of chebyshev polynomials to approximate spectral convolution
		- learn weights of linear combination to learn convolution parameters
		- approximation K-localized, only depends on nodes K steps away from node
- A neural network model based on graph convolutions can therefore be built by stacking multiple convolutional layers, each layer followed by a point-wise non-linearity

layer wise linear model
- restrict convolution to K=1. So each conv. star(g,x) is a linear function of L (normalized laplcian) passed through nonlinear activtion
- then star(g,x) = \theta'_0 x + \theta'_1 (L-I)x
	- = theta'0 x - theta'1 inv(D^0.5)Ainv(D^0.5)x
- parameters theta0 and theta1 per conv; sucessive convs (e.g. total k) convolve k^th order neighborhood

LHW -> UKU^THW -> Ug_thetaU^THW, g_theta filter -> first-order linear approximation + activation -> stack K times for Kth order neighborhood convolution

### Semi-supervised classification
layer-wise propagation allows efficient information propagation to unlabelled nodes. Now, train on labelled nodes and use structure + content to predict unlabelled. Evaluate semi-supervised classication use cross entropy error (like LR but multiple classes)

full gradient descent + sparse matrix A + dropout
featureless X if X=I

### Related work
- graph based semi supervised learning
	- graph regularization like label prop.
	- graph embedding like node2vec, deepwalk
	- problem: multi-step pipeline
- neural networks on graphs
	- Contraction maps as propagation repeatedly
	- Convolution like propagation, not scalable, node degree specific weights
	- graph as sequences with some ordering
	- spectral approaches to encode graphs
	- problems: not scalable to large graphs, does not directly encode graph structure

### Conclusion
- memory requirements not viable for large dense graphs
- equal importance to self loops and edges: A'=A+kI
- directed networks/edge orientation ignored
- approximations information loss (locality)

1. graph convolution neural network approach based on first-order fast approximation of spectral convolution on graphs to encode structure + content
2. useful embdeddings generated for semi-supervised classification
3. Methods based on graph-Laplacian regularization are most likely limited due to their assumption that edges encode mere similarity of nodes.
