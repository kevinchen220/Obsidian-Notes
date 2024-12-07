---
tags: cs484
dg-publish: true
---
# Diffusion
![[Pasted image 20241205171034.png]]
#### Add Gaussian noise and then reverse
Forward diffusion process:
* Gradually adds noise to input
Reverse denoising process:
* Learns to generate data by denoising
![[Pasted image 20241205171142.png]]

### Training Objective
![[Pasted image 20241205171209.png]]
### Network structure
Diffusion models often use U-Net architectures with ResNet blocks and [[Self-Attention Layer]] to represent $\epsilon_{\theta}(x_t, t)$
**Time representation:** Sinusoidal positional embeddings or random Fourier features
* Time features are fed to the residual blocks using either simple spatial addition or using adaptive group normalization layers
![[Pasted image 20241205171416.png]]

## Latent Diffusion Models
Map data into compressed latent space
Train diffusion model efficiently in latent space
![[Pasted image 20241205171519.png]]
##### Advantages
1. Compressed latent space: Train diffusion model in lower resolution
	1. Computationally more efficient
2. Regularized smooth / compressed latent space
	1. Easier task for diffusion model and faster sampling
3. Flexibility
	1. [[Autoencoders]] can be tailored to data

Condition information is fed into the latent diffusion model by cross-attention
Query:
* Visual features from U-Net
* Key and value: text features

## Compression and Encoding
### Diffusion Model
![[Pasted image 20241205173219.png]]
### Latent Diffusion Model
![[Pasted image 20241205173247.png]]
## Diffusion [[Transformers]]
* Replace U-Net with Transformers
![[Pasted image 20241205173830.png]]

