---
tags:
  - cs484
dg-publish: true
---
# Stochastic Gradient Descent

> [!tldr] Approximate sum using a **minibatch** of examples 32/64/128 commons

```python
# vanilla minibatch gradient descent

while True:
	data_batch = sample_training_data(data, 256) # sample 256 examples
	weights_grad = evaluate_gradient(loss_fun, data_batch, weights)
	weights += - step_size * weights_grad
```

##### SGD
$$x_{t+1} = x_t-\alpha \nabla f(x_t)$$
## Problems

> [!example]- Loss function has high **condition number**
> ![[Pasted image 20241130234104.png]]
> * step size is too big, overshooting
> * small step size converges too slow

> [!example]- What if loss function has a **local minimum** or **saddle point**?
> Zero gradient at both points so gradient descent might get stuck
> ![[Pasted image 20241130234615.png]]

> [!example]- Our gradients come from minibatches so they can be noisy!
> ![[Pasted image 20241130234833.png]]

## Solution
### SGD + Momentum
* Build up *velocity* as a running mean of gradients
* Rho gives *friction*; typically rho = 0.9 or 0.99
$$
\begin{align}
v_{t+1} &= pv_t+\nabla f(x_t)\\
x_{t+1} &= x_t-\alpha v_{t+1}
\end{align}
$$
```python
v = 0
for t in range(num_steps):
	dw = compute_gradient(w)
	v = rho * v + dw
	w -= learning_rate * v
```

> [!success]-
> * Carry us over local minima and saddle points
> * Smooth out noise from batches
> ![[Pasted image 20241201000036.png]]





