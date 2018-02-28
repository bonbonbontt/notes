## “Why Should I Trust You?” Explaining the Predictions of Any Classifier
---
### Motivation
- black box models seem to work well on unseen test data but do not necessarily
work well "in the wild". This is because it may be exploiting minor differences
in instances that are not representative of the instance classes or data leakage.
- it is important to validate the "correctness" of these models by inspection.
This is often hard to do because complex models are not interpretable.
- "if the users do not trust a model or a prediction, they will not use it". Understanding
the model means validating that model's prediction are legitimate.
    - (1) trusting a prediction, i.e. whether a user trusts an individual prediction
    sufficiently to take some action based on it,
    - (2) trusting a model, i.e. whether a user trusts all predictions of the model sufficiently
    to deploy it.
- trusting black-box models are hard since there is no direct way to evaluate the correctness
of the predictions. LIME, an algorithm that can explain the predictions of any classifier or regressor in a faithful way, by approximating it locally with an interpretable model.
- It is also hard to pick and validate predictions representative of the entire instance space.  SP-LIME, a method that selects a set of representative instances with explanations to address the “trusting the model” problem, via submodular optimization.


### LIME explanations
- interpretable: provide qualitative understanding between the interpretable input variables (e.g. bag of words, superpixels)
and the response variable. This requirement further implies that explanations should be easy to understand, which is not necessarily true of the features used by the model. Input variables” in the explanations may need to be different than the features.
- local fidelity: for an explanation to be meaningful it must at least be locally faithful, i.e. it must correspond to how the model behaves in the vicinity of the instance being predicted. identifying globally faithful explanations that are interpretable remains a challenge for complex models.
- model-agnostic: an explainer should be able to explain any model, and thus be model-agnostic

### Explaining predictions
- let G be the class of interpretable models such as linear models or decision trees
- goal is to find g in G defined over interpretable components feature space that is the
best local approximation to f, the black box function (local fidelity) with least complexity (interpretable)
- We approximate L(f, g, πx) by drawing samples, weighted by πx. We sample instances around x 0 by drawing nonzero elements ofx 0 uniformly at random (where the number of such draws is also uniformly sampled). We recover the sample in the original representation and obtain f(z)
- e.g. G: sparse linear models, L: locally weighted square loss, Pi: exponential kernel

### Explaining models
- explanation of individual predictions not sufficient to trust the model. We propose
to give a global understanding of the model by explaining a set of individual instances.
these instances need to be selected judiciously, since users may not have the time to
examine a large number of explanations.
- Given a set of instances X, we define the pick step as the task of selecting B instances for the user to inspect.
B is the user budget. This method should pick a diverse, representative set of explanations to show the user
- Pick using greedy optimization to try and cover as many interpretable features as possible, weighted by importance.

