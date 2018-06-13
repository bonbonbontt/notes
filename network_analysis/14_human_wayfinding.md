Paper: https://www-cs.stanford.edu/~jure/pubs/wayfinding-www12.pdf

This paper analyzes how humans navigate in an information network. Specifically, they analyze human navigation paths in a Wikipedia game where users have to get from page A to page B using local information (hyperlinks) using as few clicks as possible.

Players have no knowledge about the network structure; Rely on hyperlinks and similarity of visited pages w.r.t. destination page to navigate the wikipedia network. Wikipedia network has a skewed degree distribution; few high-degree nodes contribute to everything being connected by short paths.

Main finding: people find their way to the destination by first locating a high-degree node/hub and then by navigating to similar nodes (i.e. reducing conceptual distance at each step) until the user reaches the target.

Mode and median search times (in terms of number of clicks) differ from the optimal (shortest path) by 1 click and 2 clicks respectively, so human navigation using local information and "concepts" is quite efficient. This is beacuse links in wikipedia network depend on similarity & individuals have an intuitive understanding of how concepts relate to one another at multiple levels.

Relevant findings:
Users navigate to high-degree nodes in the beginning. This is because high-degree are easily reachable (even by a random walk) and connects to multiple types of pages, so users have more options.
Conceptual distance to the target page decreases after each click. This implies that users navigate based on similarity.
Users rely on both degree/popularity and similarity. Experiments show that users first rely on degree (1) and then rely on similarity (2)

Relevant related work:

P. S. Dodds, R. Muhamad, and D. J. Watts. An experimental study of search in global social networks. Science, 301(5634):827–829, 2003.

Ö. S ̧ims ̧ek and D. Jensen. Navigating networks by using homophily and degree. PNAS, 105(35):12758–12762, 2008.

----


Connections to our random walk model

Our model uses similarity-biased random walks to model how individuals navigate with local information in information networks aka human wayfinding. This paper focuses on analyzing human wayfinding whereas our project focuses on explaining macroscopic network properties by modeling human wayfinding.
The data analysis validates our choice of random walks for human wayfinding because random walks loosely incorporate both findings of the paper - tendency to visit hubs and similarity-biased navigation.
The results are based on a Wikipedia game but it can be extended to any information networks where users want to visit a target node. In the case of citation networks, the target nodes are papers that a researcher cites.
