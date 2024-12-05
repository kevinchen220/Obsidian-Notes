---
tags:
  - cs484
dg-publish: true
---
# Dropout
>[!tldr] In each forward pass, randomly set some neurons to zero
>* Probability of dropping is a [[Hyperparameters]]
>	* 0.5 is common

> [!faq] Why do we want this?
> Forces the network to have a redundant representation
> * Prevents **co-adaptation** of features
> 
> ![[Pasted image 20241202154946.png]]

Dropout is a large **ensemble** of models
* Each binary mask is one model

#### Problems: Test Time
*Dropout makes our output random!*
![[Pasted image 20241202155232.png]]
Want to “average out” randomness at test-time
$$y = f(x) = E_z[f(x,z)] = \int p(x)f(x,z)dz$$
* this integral seems hard…
> [!success] Approximate the integral
> At test time, drop nothing and **multiple by dropout probability**
> ![[Pasted image 20241202155545.png]]

#### Inverted Dropout
> [!tldr] Do the re-scaling during training time rather than test time

### Architecture
Dropout is usually applied in the fully-connected layers
* later architectures use global average pooling instead
	* they don’t use dropout
