---
dg-publish: true
tags: cs484
---
# Neural Networks

### [[Feature Extraction]]

#### Before
Linear score function: $f=Wx$
#### Now
2-layer Neural Network: $f=W_2 \max(0, W_1x)$
$W_2 \in \mathbb{R}^{C\times H}, W_1 \in \mathbb{R}^{H\times D}, x\in \mathbb{R}^D$

3-layer Neural Network: $f=W_3\max(0, W_2\max(0, W_1x))$

### [[Activation Function]]
### Fully-connected network
AKA Multi-layer perceptron
![[Pasted image 20241201101017.png]]

### Neural Net
* First layer is bank of templates
* Second layer recombines templates
![[Pasted image 20241201115009.png]]

### Deep Neural Networks
![[Pasted image 20241201115203.png]]

#### More hidden layers = more capacity
![[Pasted image 20241201120857.png]]

> [!faq]
> Are we overfitting with too many hidden layers?
> Should we reduce the number of hidden layers?
> 
> Don’t regularize with size; instead use stronger L2
> ![[Pasted image 20241201121055.png]]

> [!tldr] Universal Approximation
> A neural network with one hidden layer can approximate any function $f: R^N → R^M$ with arbitrary precision

### Examples
![[Pasted image 20241201121405.png]]

![[Pasted image 20241201121527.png]]


## Convex Function
A function $f:X \subseteq \mathbb{R}^n → \mathbb{R}$ is **convex** if for all $x_1, x_2\in X, t\in [0,1]$, $f(tx_1+(1-t)x_2) \leq tf(x_1) + (1-t)f(x_2)$
* This means that the secant line between any two points of a function always lies above the function
![[Pasted image 20241201122223.png]]
> [!tldr] A convex function is a (multidimensional) bowl
> * Easy to optimize
> * Converging to global minimum

> [!tldr] [[Linear Classification|Linear classifiers]] optimize a **convex function**
> * [[Optimization]]

> [!warning] Most neural networks need **Non-convex optimization**
> * Few or no guarantees about convergence
> * Seems to work anyways lol




