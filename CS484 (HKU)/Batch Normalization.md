---
tags:
  - cs484
dg-publish: true
---
# Batch Normalization
> [!tldr] “Normalize” the outputs of a layer so they have zero mean and unit variance

![[Pasted image 20241201235908.png]]
### Input
$x: N \times D$
![[Pasted image 20241202000042.png]]
![[Pasted image 20241202000048.png]]

> [!faq]- What if zero-mean, unit variance is too hard of a constraint?
> **Learnable scale and shift parameters:** $\gamma, \beta : D$
> ![[Pasted image 20241202000259.png]]

### Test-Time
Don’t want estimates to depend on minibatch
![[Pasted image 20241202000459.png]]

> [!important]- Usually insert batch normalization after fully connected or convolutional layers, and before nonlinearity
> ![[Pasted image 20241202000842.png]]

##### Pros
* Makes deep networks **much easier to train**
* Allows high learning rates, faster convergence
* Networks become more robust to initialization
* Acts as regularization during training
* Zero overhead at test-time: can be fused with conv!
![[Pasted image 20241202001020.png]]
##### Cons
* Not well-understood theoretically
* Behaves differently during training and testing
	* This is a very common source of bugs
* 
