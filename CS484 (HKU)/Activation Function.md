---
dg-publish: true
tags: cs484
---
# Activation Function
> [!tldr] 2-layer Neural Network: $f=W_2 \max(0, W_1x)$
> `max` is the **activation function**
> The function $ReLU(z)=max(0,z)$ is called “Rectified Linear Unit”

> [!faq]- What if we build a neural network with no activation function?
> $s = W_2W_1x$
> $W_3 = W_2W_1\in \mathbb{R}^{C\times H}$
> So we get, $s=W_3x$
> This is a [[Linear Classification|linear classifier]]

#### Examples of Activation Functions
![[Pasted image 20241201115747.png]]
>[!important] ReLU is a good default choice

### Space warping
Consider a linear transform: h = Wx where x, h are both 2-dimensional
* Not linearly separable in original space or feature space
![[Pasted image 20241201120557.png]]

Consider a neural net hidden layer:
h = ReLU(Wx) = max(0, Wx) where x, h are both 2-dimensional
* Not linearly separable in original space but **linearly separable in feature space**

![[Pasted image 20241201120736.png]]
![[Pasted image 20241201120755.png]]


