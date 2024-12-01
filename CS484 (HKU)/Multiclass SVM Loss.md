---
tags:
  - cs484
dg-publish: true
---
# Multiclass SVM Loss
> [!tldr]
> Given an example $(x_i, y_i)$ where $x_i$ is the image and $y_i$ is the label, and using the shorthand for the scores vector $s=f(x_i, W)$
> 
> The SVM loss has the form
> $$L_i=\sum_{j\neq y_i}\max(0,s_j-s_{y_i}+1)$$

```python
def L_i_vectorized(x, y, w):
	scores = W.dot(x)
	margins = np.maximum(0, scores - scores[y] + 1)
	margins[y] = 0
	loss_i = np.sum(margins)
	return loss_i
```

**Loss over full dataset is average of each loss**

![[Pasted image 20241130153942.png]]

### Example
![[Pasted image 20241130154230.png]]
> [!faq]- What happens if we change the score a bit of the car image?
> If changing just a little, nothing will change since car score is more than 1 larger than other scores

> [!faq]- What is the min/max possible loss
Min is 0, max is infinite

> [!faq]- At initialization W is small so all s is approximately 0. What is the loss?
> Number of classes - 1
> Since summing all the wrong classes, each loss is 1

> [!faq]- What if the sum was over all classes (including the correct class)?
> The loss score would be +1

> [!faq]- What if we use mean instead of sum?
> Does not change anything since we are scaling by a constant

>[!faq]- Suppose we found a W such that L = 0. Is this W unique?
>No! 2W also has L=0






