---
tags: cs484
dg-publish: true
---
# Linear Classification
### Parametric Approach
**Image → f(x, W) → Class scores**
* Image: Array of 32x32x3 numbers
	* 3072 numbers total
	* 32 by 32 image with RGB channels
* W: parameters or weights
> [!success] Don’t need training data at test time
> A lot more scalable

![[Pasted image 20241129164249.png]]
* e.g. 10 class scores for cifar-10

> [!tldr] Linear classifier will draw out lines to separate each category

![[Pasted image 20241129165315.png]]

### Limitations
![[Pasted image 20241129165342.png]]