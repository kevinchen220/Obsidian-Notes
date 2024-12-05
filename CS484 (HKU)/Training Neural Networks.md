---
tags:
  - cs484
  - unit
dg-publish: true
---
# Training Neural Networks
## Overview
1. **One time setup**
	1. Activation functions
	2. Data pre-processing
	3. Weight Initialization
	4. Regularization
2. **Training Dynamics**
	1. Learning rate schedules
	2. Large-batch training
	3. [[Hyperparameters]] optimization
3. **After training**
	1. Model ensembles
	2. Transfer learning

## [[Activation function]]
![[Pasted image 20241202142256.png]]

## [[Data Preprocessing]]
* Transform data for efficient training

## [[Weight Initialization]]

## [[Regularization]]
Common:
* [[Dropout]]
	* Consider if there are large fully-connected layers
* [[Batch Normalization]]
	* Almost always a good idea
* [[Data Augmentation]]
* Cutout
	* Cut out parts of the image
* Mixup
	* Mix up two images

*Try cutout and mixup for small classification datasets*

## [[Learning Rate]]
SGD, SGD + Momentum, Adagrad, RMSProp, Adam all have **[[learning rate]]** as a [[Hyperparameters]]

## [[Early Stopping]]
*How long to train?*

## [[Choosing Hyperparameters]]

## [[Model Ensembles]]
## [[Transfer Learning]]

