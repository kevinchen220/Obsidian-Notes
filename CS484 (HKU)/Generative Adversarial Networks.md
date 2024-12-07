---
tags: cs484
dg-publish: true
---
# Generative Adversarial Networks
**Setup:** Assume we have data $x_i$ drawn from distribution $p_{\text{data}}(x)$. Want to sample from $p_{\text{data}}$
**Idea:** Introduce a latent variable z with simple prior p(z). Sample z ~ p(z) and pass to a **Generator Network** x = G(z).
Then x is a sample from the **Generator distribution** $p_G$. Want $p_G = p_{\text{data}}$

**Generator Network:** Try to fool the discriminator by generating real-looking images
**Discriminator Network:** Try to distinguish between real and fake images

![[Pasted image 20241205162806.png]]
**Jointly train Generator network and Discriminator Network**
Train jointly in **minimax game**
* Discriminator wants to $D(x) = 1$ for real data and $D(x) = 0$ for fake data
* Generator wants $D(x) = 1$ for fake data
![[Pasted image 20241205165129.png]]
##### Train G and D using alternating gradient updates
![[Pasted image 20241205165259.png]]
At start of training, generator is very bad and discriminator can easily tell apart real from fake
* so D(G(z)) close to 0
> [!warning] Vanishing gradients for G

>[!success] Train G to maximize -log(D(G(Z)))
>* Instead of minimize log(1-D(G(z)))
>* G gets strong gradients at start of training
![[Pasted image 20241205165906.png]]

## Architecture: DC-GAN
**Generator** is an upsampling [[Convolutional Neural Networks|convolutional network]]
**Discriminator** is a convolutional network
![[Pasted image 20241205170313.png]]
## Vector Math
![[Pasted image 20241205170613.png]]
![[Pasted image 20241205170621.png]]
