# Beyond Assortativity: Proclivity index for attributed networks

given network structure and content, which attributes and pairs of attributes show correlation?

## Limitations of assortativity
- assortativity measures the structural correlation of a single attribute, not pairs of attributes
- it can only capture the mixing pattern w.r.t to the same attribute value of an attribute
- cannot properly distinguish between randomness and heterophily
- cannot measure mixing pattern between 2 different attribute values of the an attribute or 2 different attribute values of different attributes

not a thorough evaluation metric to analyze mixing patterns in attributed networks

## Proclivity definition

1. self-proclivity captures predictability of neighbor's attribute value for A given attribute value of node
2. cross-proclivity captures predictability of neighbor's attribute value for B given node's attribute value for B

## Related work
1. Modularity
2. Assortativity (normalized modularity for nominal attributes)
3. QA-Index (Extension of assortativity for vector-valued attributes)

## Proclivity
suppose attribute A and B (B is A for self-proc.) have m and n attribute values respectively. then M is the m by n mixing matrix with M_{ij} equal to the number of edges connecting nodes with i^th value of attr. A and j^th value of attr. B.

Mixing matrix: https://slack-files.com/T04E4BQPP-F5HF37GPN-4da1e75109

Prone_f: https://slack-files.com/T04E4BQPP-F5J7X3B1U-e9cc5e34de

example 1: https://slack-files.com/T04E4BQPP-F5HDN3T8S-d3030cdc12

example 2: https://slack-files.com/T04E4BQPP-F5HF4JW3E-4b86fdefa8

## Properties

- Prone is more general than assortativity as you can compare pairs of attributes
- Prone equals 0 if there is no structural correlation w.r.t attribute or pair of attributes
- Prone equals 1 if there is perfect self or cross proclivity
- Can be computed in linear time

Unlike assortativity, which only focuses on the diagnoal elements of the confusion matrix, proclivity computes the normalized average divergence along rows and columns.

## Other relevant papers

1. User similarities on social networks (Akcora)
3. Randomization test to distinguish homophily and influence (Neville)
5. Mining attribute-structure correlated patterns in large attributed graphs (Silva)
4. MAG (Leskovec) and SAN (Song)
