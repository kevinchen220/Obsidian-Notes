---
tags:
  - cs484
dg-publish: true
---
# Data Preprocessing
![[Pasted image 20241202150857.png]]
Standardize data some way
* Pull closer to origin
	* subtract by mean
* Each feature has same variance
	* Divide by standard deviation
#### Other Methods
![[Pasted image 20241202151143.png]]

**Before Normalization**
![[Pasted image 20241202151307.png]]
Classification loss very sensitive to changes in weight matrix
* Hard to optimize

**After Normalization**
![[Pasted image 20241202151317.png]]
Less sensitive to small changes in weights
* Easier to optimize

> [!example] Data Preprocessing for Images
> Consider CIFAR-10 example with [32, 32, 3] images
> * Subtract the mean image (AlexNet)
> 	* Mean image = [32, 32, 3] array
> * Subtract per-channel mean (VGGNet)
> 	* Mean along each channel = 3 numbers
> * Subtract per-channel mean and divide by per-channel std (ResNet)
> 	* mean along each channel = 3 numbers


> 