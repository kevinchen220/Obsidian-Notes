---
dg-publish: true
tags:
  - cs484
---
# Learning Rate
[[Stochastic Gradient Descent]], [[AdaGrad]], [[Adam]] all have learning rate as a [[Hyperparameters|hyperparameter]]

![[Pasted image 20241201002807.png]]
> [!faq] Which one of these learning rates is best to use?
> **All of them!** Start with large learning rate and decay over time

### Learning Rate Decay
![[Pasted image 20241201003148.png]]
Reduce learning rate at a few fixed points.
* E.g. for resNets, Multiply LR by 0,1 after epochs 30, 60, and 90.
Examples of decay:
* Cosine $\alpha_t = \frac{1}{2}\alpha_0(1+\cos(t\pi/T))$
	* Two [[Hyperparameters]]
	* No new hyperparameters
![[Pasted image 20241202165242.png]]
* Linear $\alpha_t = \alpha_0(1-t/T)$
![[Pasted image 20241202165421.png]]
* Inverse sqrt $\alpha_t = \alpha_0 / \sqrt{t}$
	* Not a lot of time in high learning rate
	* A lot of time in low learning rate
![[Pasted image 20241202165449.png]]
* constant $\alpha_t = \alpha_0$
	* Works well most of the time
![[Pasted image 20241202165721.png]]

### Linear warmup
> [!tldr] High initial learning rates can make loss explode
> Linearly increasing learning rate from 0 over the first ~5000 iterations can prevent this
> ![[Pasted image 20241201003120.png]]

