# Backpropagation
![[Pasted image 20241201193612.png]]
#### Tedious to derive $\nabla_WL$ on paper
* Need to re-derive if we change the loss function

## Use a [[Computational Graph]]

> [!example]-
> ![[Pasted image 20241201200359.png]]
> 1. **Forward pass**: Compute outputs
> 	1. $q=x+y$, $f = qz$
> 2. **Backward pass**: Compute derivatives
> 	1. Want $\frac{\partial f}{\partial x}$, $\frac{\partial f}{\partial y}$, $\frac{\partial f}{\partial z}$
> 
> $\frac{\partial f}{\partial f} = 1$
> $\frac{\partial f}{\partial z} = q = 3$
> $\frac{\partial f}{\partial q} = z = -4$
> $\frac{\partial f}{\partial y} = \frac{\partial q}{\partial y} \frac{\partial f}{\partial q} = -4$ (**Chain Rule**) ($\frac{\partial q}{\partial y} = 1$)
> $\frac{\partial f}{\partial x} = \frac{\partial q}{\partial x} \frac{\partial f}{\partial q} = -4$ (**Chain Rule**) ($\frac{\partial q}{\partial x} = 1$)
> 
> ![[Pasted image 20241201201631.png]]

![[Pasted image 20241201201755.png]]

> [!example]-
> ![[Pasted image 20241201202504.png]]

> [!important]- We can define our own nodes
> ![[Pasted image 20241201202637.png]]

### Patterns
**Add gate**: gradient distributor
* Can copy gradient from upstream to downstream
* ![[Pasted image 20241201202756.png]]
**Copy gate**: gradient adder
* Add upstream gradient to get downstream gradient
* ![[Pasted image 20241201202852.png]]
**Multiplication gate**: “swap multiplier”
* Downstream gradient is upstream gradient times other input
* ![[Pasted image 20241201202931.png]]
**Max gate**: gradient router
* Route gradient to max input, 0 otherwise
* ![[Pasted image 20241201203005.png]]
* 


> [!faq] What about backprop with vector-valued functions?
> ![[Pasted image 20241201210302.png]]

## Backprop with vectors
![[Pasted image 20241201211206.png]]
> [!example]-
> **ReLU**
> ![[Pasted image 20241201212825.png]]
> Want implicit way to express Jacobian as only diagonal is useful, rest is filled with 0s
> ![[Pasted image 20241201212942.png]]

## Backprop with Matrices (or Tensors)
![[Pasted image 20241201213252.png]]
> [!example]-
> ![[Pasted image 20241201220315.png]]



