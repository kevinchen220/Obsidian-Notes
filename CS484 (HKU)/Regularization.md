---
tags:
  - cs484
dg-publish: true
---
# Regularization
> [!tldr] Prevents overfitting
> Model should be “simple”, so it works on test data

Regularization term: $\lambda R(W)$
$$L=\frac{1}{N}\sum_iL_i(f(x_i,W), y_i) + \lambda R(W)$$

$\lambda$ = regularization strength ([[Hyperparameters]])

## Common use:
* [[L2 Regularization]]
* [[L1 Regularization]]
* [[Elastic net]]
* [[Max norm regularization]]
* [[Dropout]]
* [[Batch Normalization]]
* [[Data Augmentation]]

## A common pattern
#### Training
Add some kind of randomness
#### Testing
Average out randomness
* Sometimes approximate

