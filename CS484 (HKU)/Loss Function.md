---
tags: cs484
dg-publish: true
---
# Loss Function

> [!tldr] A **loss function** tells us how good our current classifier is
> Given a dataset of examples
> $$\{(x-i,y_i)\}^{N}_{i=1}$$
> Where $x_i$ is image and $y_i$ is label
> Loss over the dataset is a sum of loss over examples:
> $$L=\frac{1}{N}\sum_iL_i(f(x_i,W), y_i)$$

### [[Regularization]]
Regularization term: $\lambda R(W)$
$$L=\frac{1}{N}\sum_iL_i(f(x_i,W), y_i) + \lambda R(W)$$

## Examples of loss functions
#### [[Multiclass SVM Loss]]
#### [[Softmax Classifier|Multinomial Logistic Regression]]


