## Homophily and the Glass Ceiling Effect in Social Networks
---
### Motivation
- The glass ceiling effect has been defined in a recent US Federal Commission report as “the unseen, yet unbreakable barrier that keeps minorities and women from rising to the up- per rungs of the corporate ladder, regardless of their qualifications or achievements”.
- propose a natural mathematical model, called the biased preferential attachment model, that partially explains the causes of the glass ceiling effect. (PA applied to majority-minority bipopulated homophilic network)
- model accommodates three well known social phenomena: (i) the “rich get richer” mechanism, (ii) a minority-majority partition, and (iii) homophily. We prove that our model exhibits a strong moment glass ceiling effect and that all three conditions are necessary,

### Model
- G(n,r,p): n nodes, r fraction of them are minority, p level of homophily (p=0 heterophily, p=1 homophily) over time. node selected
using PA and edge formed with probability p if same color else 1-p. If selection rejected, retry.

### Glass ceiling example
- With time, new PhD students arrive, but for some fields female students arrive at a lower rate than male students. Upon arrival, each student needs to select exactly one mentor, where the selection process is governed by the mechanisms of preferential attachment and homophily. Namely, initially the student selects the mentor according to the rules of preferential attachment and then homophily takes its role, rejecting the selection with some probability if their gender is different and forcing a re-selection. Over time, graduated students may become mentors and some mentors become more successful than others.
- The only tiny (but ominous) sign for the potential dangers of this homophilic effect is that it does affect the professor: a male professor who rejects (or is rejected by) some fraction of the female candidates risks little, whereas a female professor who rejects (or is rejected by) some fraction of the male candidates will eventually have fewer students overall, since most of the applicants are male.

### Results
- power inequality: the ratio of average degree of minority nodes to the average degree of majority nodes can be
bounded by a constant c < 1. (on average, majority nodes have more social capital)
- Tail glass ceiling: as n increases, the ratio of the number of minority nodes that have degree > k
and the number of majority nodes that have degree > k goes to 0. (as network increases, visibility of
minority nodes decreases)
- Moment glass ceiling: ratio of sum of degree squared divided by total {minority, majority} nodes goes to 0
- G(n,r,p) exhibits all three ceilings/inequalities; PA selection, 0 < p < 1 and r < 0.5 necessary for moment
glass ceiling.

### Proof sketch
- basic idea: degree distribution of minority and majority nodes follow power law with different exponents. Once this is established, it is simple to derive the glass ceiling effect for the population with a higher exponent in the degree distribution
- show that alpha_t (ratio of degree of minority nodes) converges. Derive expectation and use doob martingale + azuma to show that
alpha_t concentrated around E[alpha_t].
- empirical evidence: DBLP mentor-student network, male vs. female glass ceiling. 

