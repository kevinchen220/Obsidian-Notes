---
tags: cs484
dg-publish: true
---
# Softmax Classifier
AKA **Multinomial Logistic Regression**, **Cross-entropy loss**

> [!tldr] Want to interpret raw classifier scores as **probabilities**

### Softmax Function
$$s=f(x_i;W)$$
$$P(Y=k|X=x_i)=\frac{e^sk}{\sum_je^sj}$$
$$L_i=-\log P(Y=y_i|X=x_i)$$
**Maximum Likelihood Estimation**: Choose weights to maximize the likelihood of the observed data

![[Pasted image 20241130142946.png]]