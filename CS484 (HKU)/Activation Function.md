---
dg-publish: true
tags:
  - cs484
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


## Sigmoid
![[Pasted image 20241202142410.png]]
$$\sigma(x)=1/(1+e^{-x})$$
* Squashes number to range [0,1]
* Historically popular since they have nice interpretation as a saturating “firing rate” of a neuron
> [!warning] 3 Problems
> 1. Saturate neurons “kill” the gradients
> 	1. Flat areas kill the gradient
> 2. Sigmoid outputs are not zero-centered
> 	1. Always all positive or all negative
> 3. exp() is a bit compute expensive

## Tanh
> [!tldr] Shifted sigmoid
![[Pasted image 20241202143625.png]]
* Squashes numbers to range [-1, 1]
* zero centered (nice)
* still kills gradients when saturated

## ReLU (Rectified Linear Unit)
![[Pasted image 20241202143737.png]]
* Does not saturate (in +ve region)
* Very computationally efficient
* Converges much faster

> [!warning] Problems
> * Not zero-centered output
>  > [!faq] What happens when x < 0?
> > Gradient will be identically 0
> > * Learning cannot proceed
>   >
> > *Dead ReLU*
> > * will never activate/update

> [!success] Sometimes initialize ReLU neurons with slightly positive bias

## Leaky ReLU
![[Pasted image 20241202144437.png]]
* Does not saturate
* Computationally efficient
* Converges much fast
* **Will not “die”**
* `0.01` is a [[Hyperparameters]]
## Parametric ReLU (PReLU)
$$f(x) = max(\alpha x, x)$$

## Exponential Linear Unit (ELU)
![[Pasted image 20241202145325.png]]
* All benefits of ReLU
* Closer to zero mean outputs
* Negative saturation regime compared with Leaky ReLU
	* Adds some robustness to noise
> [!warning] Computation requires exp()

## Scaled Exponential Linear Unit (SELU)
![[Pasted image 20241202145336.png]]
* Scaled version of ELU that works better for deep networks
* “Self-Normalizing” property
	* Can train deep SELU networks without [[Batch Normalization]]

## Comparison
![[Pasted image 20241202145850.png]]
* Inconsistent results
> [!tldr] Just use **ReLU**
> * Try out Leaky ReLU / ELU / SELU / GELU if you need to squeeze that last 0.1%
> * *Don’t use sigmoid or tanh*



