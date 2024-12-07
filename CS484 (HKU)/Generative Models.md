---
dg-publish: true
tags:
  - cs484
  - unit
---
# Generative Models
## Supervised VS. Self-supervised Learning
### Supervised Learning
**Data:** (x, y)
* x is data, y is label
**Goal:** Learn a **function** to map x → y
**Examples:** Classification, regression, objection detection, etc.

### Self-supervised Learning
**Data:** x
* Just data, no labels
**Goal:** Learn some underlying hidden structure of the data
**Examples:** Clustering, dimensionality reduction, feature learning, density estimation, etc.

## Generative Modeling
Given training data, generate new samples from same distribution
![[Pasted image 20241205155102.png]]
1. Learn $p_{\text{model}}(x)$ that approximates $p_{\text{data}}(x)$
2. Sampling new x from $p_{\text{model}}(x)$

## [[Fully visible belief network (FVBN)]]
## [[Autoencoders]]
## [[Generative Adversarial Networks]]
## [[Diffusion]]

