# Growing a graph matching from a handful of seeds

## Introduction

### contribution
- new matching algorithm that requires fewer seeds
- very robust to incorrect matchings, but at the cost of few matching errors
- In summary, we manage to trade off a very significant reduction in the seed set size with a fairly benign increase in the error rate

### graph matching (1)
- generalization of graph isopmorphism, relies only on link structure
- **matching: bijection between full or partial vertex sets of the 2 graphs using only link structure**
- applications: security de-anonymization, protein network alignment and computer vision
- most approaches use percolation theory, start from (very few) matched seeds and infect neighborhoods until most matched
- existing algorithms very sensitive to size and correctness of seed set
- The matching is generated incrementally, starting from the seed pairs and percolating to other node pairs; for this reason, we refer to this class of algorithms as Percolation Graph Matching (PGM) methods.
- strong senstivitiy to seed size; too small, the percolation did not take off; when increased, abrupt change to a supercritical regime, where the algorithm succeeded in de-anonymizing a large fraction of the network
- **In every step, the set of node pairs matched so far are used as evidence to match an additional node pair, if possible.**

### main idea
- there is a tradeoff between accuracy/correctness of matching and the number of matches made by PGM. One bad match can have a cascading effect since new matches are found by using matched pairs. On the other hand, have a strong evidence threshold to match a pair can restrict the percolation.
- New algo breaks the tradeoff by decoupling the decision of matching a candidate pair based on evidence and deciding on whether or not to use a candidate pair as evidence. This allows the algo to match more pairs without incorrectly matching because of previous wrong matches
	- requires fewer seed matches and more robust to errors

### notation
-  A pair [i′, j′] ∈ V1 ×V2 is a neighbour of another pair [i, j] if (i, i′) ∈ E1 and (j, j′) ∈ E2. In the description of the matching algorithms, we refer to a pair [i,j] spreading out marks as adding one mark to each neighbouring pair of [i,j]. The score of a pair is defined as the number of marks it received from other pairs so far.
- the hidden correct mapping be- tween the nodes in V0 is the identity mapping
- Let Λ(S) denote the number of correct pairs in a set S of pairs, and let Ψ(S) represent the number of wrong pairs

### PercolatedMatched (related work)
-  at each time step τ, the algorithm picks an unused pair from set A and spread marks to all of its neighbouring pairs; (iii) as soon as a pair obtains at least r marks, i.e., it is a neighbour of at least r used pairs
- in the set A, it will be added to the set A; and (iv) the algorithm stops when there exist no further unused pairs in the set A.

## Algorithm, Synthetic model

### **Correlated Random Graph Model (Sythetic network for analysis)**
- G(n,p; t,s) first generates G(n,p) ER to then generate G1 and G2 with partially overlapping vertex sets
- filter vertex set of G with probability t for G1 (V1) and G2 (V2)
- for all pairs of nodes in V1/V2 that have edges in G/E, sample each edge between pair with probability s
- **goal: identify mapping between nodes in intersection of vertex sets**


### NoisySeeds algorithm
- starts with an initial noisy seed set A0, i.e., a set with possibly many wrong pairs
- spread marks from pairs in A0 and add A0 pairs to Z used pairs set
-  If there is any pair with score at least r, then we add this pair to the matched set M.
- Each time a pair [i,j] ∈ M \ Z is chosen randomly, it spreads marks to its neighbouring pairs and is added to Z
- As the pair [i,j] is in the matching M, any other pair in the form of [i,j′] or [i′,j] is not a candidate for matching any longer and is permanently removed

### **expand once algorithm**
- expands seed set to a larger seed set and then starts PGM
- algorithm
	- for all pairs [i,j] in initial seed set A0
		- for all neighboring pairs [i', j'] of [i,j]
			- if size of A0' < max_size and no pair conflict
				- add [i', j'] to A0'
	- return A0'
- noisy seed adds a lot of pairs to initial set, which improves the chance of proper percolation but at the cost of adding many incorrectly matched pairs

## Why it works

### **intuition behind robustness**
let known matched pair be [i,j]. The neighor pair be [i', j'] such that (i,i') \in E1 and (j,j') in E2.
- suppose [i,j] match is correct. Then the neighborhood of i and j are "correct"/same too. The probability that candidate [i',j'] is marked is p*s^2.
	- p because they are ultimately the same edge generated once in the original network
	- s^2 because they are in G1 and G2.
- suppose [i,j] match is wrong or that [i,j] is correct but [i', j'] match is wrong. In either case, the probability that [i',j'] is marked is p^2*s^2.
	- p^2 because the 2 edges actually are mismatched and different. since there are 2 in G, p^2
	- s^2 same reason, in G1 and G2

So, the probability of a correct pair being marked once is much more that that of an incorrect pair. P(marked twice): p^2*s^4 vs. p^4*s^4. Only few wrong pairs with more than 2 marks: O(n1^2n2^2p^4s^4)

## Empirical results, heurisitics

### **expand when heuristic to improve perfomance on real networks**
- The robustness arguments of Sec- tion 4 allow PGM algorithms to be much more aggressive in spreading out marks
- A main feature: expand the seed set by many noisy candidate pairs whenever there are no other unused matched pairs
- Whenever there are no further pairs with score at least two, we add all the unused, unmatched neighbouring pairs of all the matched pairs to the candidate pairs
	- most are wrong but effect negligible
	- some are correct and help percolation by increasing size
- we further make the following modification. At each time step, instead of adding all the candidate pairs with score at least two to the matched set, we choose the one with the highest score among such pairs and add it to the matched
	- tie break with pairs that min. abs deg diff

### **empirical analysis**
- real world networks have more structural variance (degree, clsutering, communities) than ER graphs. So if algorithm performs well on ER, it'll likely perform well on real networks too
- precision is better than recall in all experiments. Percolation stops at some point, which is why recall is low.
- Our experiments show that choosing seeds among high– degree nodes, instead of picking them randomly, results in better matchings.
- clustering and motif-based counts

## Misc

### Questions
1. why are seeds so important? can we not find them using some algorithm? start with high deg first (low prob) and check
	- because it is not necessary that correctly matched pair has same degree even. G(n,p; t,s) so exact same node in G1 and G2 can have slightly different
2. correct matches must be marked at least twice, so it must have degree 2 at least. what about degree 1 nodes?
3. unfair comparison? use seed size after expansion and then compare?

### **Clarifications**
- it is not necessary for same node to have exactly same neighborhood. missing edges and nodes possible

### Assumptions
- A: node in G1 and G2 refer to entity, and entity links/behaves similarly in both networks
- A: model analysis is only focuses on generating G1 and G2 using parameters t,p.. does the model work well if other sampling methods used?

### Doubts
- why is P([i,j] in P_{2,cip}) = O(w^2 n p^3 s^3) when u1=v1, u2=v2
