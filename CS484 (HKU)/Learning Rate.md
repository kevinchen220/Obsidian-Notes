---
dg-publish: true
tags: cs484
---
# Learning Rate
[[Stochastic Gradient Descent]], [[AdaGrad]], [[Adam]] all have learning rate as a [[Hyperparameters|hyperparameter]]

![[Pasted image 20241201002807.png]]


### Learning Rate Decay
![[Pasted image 20241201003148.png]]
Reduce learning rate at a few fixed points.
* E.g. for resNets, Multiply LR by 0,1 after epochs 30, 60, and 90.
Examples of decay:
* Cosine
* Linear
* Inverse sqrt

### Linear warmup
> [!tldr] High initial learning rates can make loss explode
> Linearly increasing learning rate from 0 over the first ~5000 iterations can prevent this
> ![[Pasted image 20241201003120.png]]

