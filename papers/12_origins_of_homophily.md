## Origins of Homophily in an Evolving Social Network
---

Link: https://research.google.com/pubs/pub35626.html

### Overview
- This paper thoroughly analyzes the role of homophily in tie formation
as a function of similarity and structural proximity using a real-world
multi-attributed dynamic communication (email) network dataset.
- As expected,
similarity increases the probability of tie formation.
- Moreover, tie formation is
heavily biased towards triadic and focal closure. Selection to a friend of a friend
(FOF) is due to individual preferences and structural proximity.
- mutual reinforcement of tie formations due to preferences and proximity
give rise to a positive correlation between node similarity and network distance.
- structural proximity can be proxy for unobserved attributes/preferences.

### Motivation
- similarity increases likelihood of tie formation. However, individual
choice is heavily constrained by factors such as location, occupation, time
commitment, workplace location etc. These factors act as structural constraints
in a social network.
- two homophily mechanisms: choice homophily (individual preferences, intrinsic
nodal attributes) and induced homophily (increased structural opportunities to
form edges). Difficult to distinguish between the two because social environment
is affected by individual choices and vice versa.
- This is important and relevant to datasets with limited attributed information:
effects of structural proximity can be a proxy for unobserved individual prefernces.
- strong interplay between structure and agency that reinforce over time. E.g. one's
position in a network depends on choices of previous relationships, which in turn
are formed because of similarity, which in turn is formed because of position and so on.
- this paper focuses on the origins of homophily in networks. Specifically,
it studies the role of structure and individual choice in tie formation.

### Dataset
- dataset: dynamic university email network. attributes: status, gender, age,
department, years in community etc. Sliding window technique used to study edge
formation over time.
- important: email communication must be two-way for an
edge to be formed. This is different from tie formation in other kinds of networks:
OSNs, citation etc.

### Analysis

#### Tie formation
- tie formation mechanisms studied: cyclic closure (generalization of triadic closure,
useful for random walk empirical analysis). focal closure (common foci - groups, memberships etc). Shared classes are explicit foci. Bulk emails are implicit foci (but not all). Treated as one (explicit/implicit) after some calibration.
- F1: probability of new ties decreases exponentially as a function of network distance
- F2: sharing an explicit foci and sharing a friend have similar effect on tie formation. 50 times more likely than random.
- aggregate multi-attribute measure of similarity: number of attribute value matches (0 to 6)
- F3: average pairwise similarity decreases as network distance increases
- F4: average similarity increases as number of shared foci increases
- In other words, the usual result that friends are more similar than strangers can be seen as a special case of a more general rule that individuals who are “close” are more similar.
- Possible problem: similarity and foci have positive correlation fixed by controlling
for number of shared classes. Potential for differences in similarity to impact tie
formation is not diminished for pairs who share classes.

#### Effect of similarity on tie formation
- estimate the impact of similarity on probability of edge formation p(i,j) using
logistic regression: log(p/(1-p)) = b_0 + b_1 Sim.
- e^{b_1} gives odd ratio: (p(tie|sim=1)/p(no tie|sim=1))/(p(tie|sim=0)/p(no tie|sim=0)) which is approximately p(new tie|sim=1)/p(new tie|sim=0) because p(no tie|sim) is roughly equal to p(tie|sim). e.g. if e^b1 = 1.6, then 1.6 times more likely is sim=1 instead of
sim =0 which is roughly 1.6^6=50 times more likely if highly similar (s=6)
- important: logistic regression fit on different subsets of data to control for foci,
structure proximity; better interpretability
- shared foci or small distance (d=2) reduces odds ratio to 1.03-126; Thus, although similarity continues to play an important role in new tie formation even when it is brokered by a mutual acquaintance, once again the restricted opportunities afforded by structural proximity appear to account for much of the process of selecting alters.

#### Effect of similarity to risk sets
- risk set: set of individuals with whom any given individual A is “at risk” (i.e., has a high probability) of forming a tie — in particular, individuals with whom A shares either a social focus or a mutual acquaintance
- two risk sets: individuals at distance 2, individuals sharing social foci (binary variable). F5: 60% and 30% of all ties are formed by triadic closure and focal closure respectively.
- F6: examine effect of similarity on node transitioning from d > 2 to d = 2 (risk set)
and of node joining shared focus by fitting logistic regression models. In FOF (d=2)
similar individuals are more likely to be at d=2 (1.6 times more likely per increase in similarity).
    - F7: strong dependency on similarity in P(d > 2 to d=2) disappears by controlling for shared focus i.e. similarity does not tie formation significantly if pair is close and in shared focus.
- F8: P(same implit focus in spring sem) strongly depends on similarity (2.6x) if not
shared in fall sem and (1.2x) if shared in fall sem.
    - F9: strong dependency on similarity in P(same focus) disappears by controlling for distance (friend OR FOF).

### Discussion
- triadic closure and focal closure are as important as similarity. these mechanisms
act as structural constraints that limit the search space of individuals.
- C1: individuals who are “proximate” in the network, because they either are connected by a short path length or share a social focus, are more similar than those who are “distant"
- C2: the importance of similarity is strongly mitigated by accounting for network distance or shared foci. individuals.
- C3: In other words, structural constraints that may initially appear exogenous are in fact generated endogenously and act effectively as proxies for unobserved individual preferences.
- C4: As the network and structure coevolve (McPherson and Ranger-Moore 1991), distant but similar individuals will be brought closer to each other in the network, creating a positive correlation between similarity and proximity.
