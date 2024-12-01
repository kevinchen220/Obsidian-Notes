---
tags:
  - cs484
dg-publish: true
---
# [[Gradient]] Descent

```python
# Vanilla gradient descent

while True:
	weights_grad = evaluate_gradient(loss_fun, data, weights)
	weights += - step_size * weights_grad
```

`step_size`/learning rate is [[Hyperparameters]]

$$L=\frac{1}{N}\sum_iL_i(f(x_i,W), y_i) + \lambda R(W)$$
$$\nabla_W L=\frac{1}{N}\sum_i\nabla_WL_i(f(x_i,W), y_i) + \lambda\nabla_WR(W)$$

Full sum expensive when N is large!

Approximate sum using a **minibatch** of examples 32/64/128 commons: [[Stochastic Gradient Descent]]
