---
tags: cs484
dg-publish: true
---
# Fully visible belief network (FVBN)
#### Explicit density model
$$p(x)  = p(x_1, x_2, ..., x_n)$$
* $p(x)$ = likelihood of image x
* $p(x_1, x_2, ..., x_n)$ = joint likelihood of each pixel in the image
Use chain rule to decompose likelihood of an image x into product of 1-d distributions
![[Pasted image 20241205155534.png]]
Then, maximize likelihood of training data
## Pixel[[Recurrent Neural Networks|RNN]]
1. Generate image pixels one at a time, starting at the upper left corner
2. Compute a hidden state for each pixel that depends on hidden states and RGB values from the left and from above
3. At each pixel, predict red, then blue, then green
	1. Softmax over [0, 1, …, 255]
> [!warning] Sequential generation is slow!

Each pixel depends implicitly on all pixels above and to the left
![[Pasted image 20241205160746.png]]


## Pixel[[Convolutional Neural Networks|CNN]]
1. Still generate image pixels starting from corner
2. Dependency on previous pixels now modelled using a CNN over context region (masked convolution)
Training faster than PixelRNN
Generation still sequential → slow
![[Pasted image 20241205160941.png]]

> [!success] Pros
> * Can explicitly compute likelihood p(x)
> * Explicit likelihood of training data gives good evaluation metric
> * Good samples

> [!warning] Cons
> * Sequential generation → slow

Improving PixelCNN performance
* Gated convolutional layers
* Short-cut connections
* Discretized logistic loss
* Multi-scale
* Training tricks
* Etc…