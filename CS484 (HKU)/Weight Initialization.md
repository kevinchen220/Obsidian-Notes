---
tags:
  - cs484
dg-publish: true
---
# Weight Initialization
![[Pasted image 20241202151734.png]]
> [!faq] What happens if we initialize all W = 0, b = 0?
> * Outputs are all going to be 0
> * Outputs will not depend on inputs
> * Gradients will all be 0
>   
> **BAD!!!**

#### Initialize with **small random numbers**
Gaussian with zero mean, std=0.01
```python
W = 0.01 * np.random.randn(Din, Dout)
```
*Works ok for small networks, but problems with deeper networks*
* All activations tend to zero for deeper network layers
* Gradients all zero
	* No learning

![[Pasted image 20241202152155.png]]
Try larger number (0.01 → 0.05)
```python
W = 0.05 * np.random.randn(Din, Dout)
```
Too large
* Activations are in saturated regimes
* Local gradients all zero
	* No learning
![[Pasted image 20241202152413.png]]

### Xavier Initialization
```python
W = np.random.randn(Din, Dout) / np.sqrt(Din)
```
* For conv layers, `Din` is `kernel_size ** 2 * input_channels`
Activations are nicely scaled for all layers!
![[Pasted image 20241202152805.png]]

> [!faq] What about ReLU?
> Xavier assumes zero centered activation function
> *Activations collapse to zero again*
> * No learning
> ![[Pasted image 20241202153237.png]]

### Kaiming / MSRA Initialization (ReLU)
```python
W = np.random.randn(Din, Dout) / np.sqrt(2 / Din)
```
**ReLU correction:** std = sqrt(2 / Din)
![[Pasted image 20241202153350.png]]

### [[CNN Architectures#Residual Networks|Residual Networks]]
![[Pasted image 20241202153613.png]]
If we initialize with MSRA, then Var(F(x)) = Var(x)
But then Var(F(x) + x) > Var(x)
* Variance grows with each block
>[!success] Solution
> Initialize first conv with MSRA, initialize second conv to zero
> Then, Var(x + F(x)) = Var(x)
