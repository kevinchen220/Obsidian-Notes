---
tags:
  - cs484
  - unit
dg-publish: true
---
# CNN Architectures
## AlexNet (8 Layers)
* 227 x 227 inputs
* 5 [[Convolution Layers]]
* [[Pooling Layers#Max Pooling|Max Pooling]]
* 3 fully-connected layers
* ReLU Non-linearities
> [!important]
> ![[Pasted image 20241202124640.png]]

>[!tldr] Trends
>![[Pasted image 20241202125552.png]]

## ZFNet: A Bigger AlexNet (8 Layers)
> [!tldr] More trial and error
> Bigger networks work better?

## VGG (19 Layers)
#### Design rules
* All conv are 3x3 stride 1 pad 1
* All max pool are 2x2 stride 2
* After pool, double number of channels
Network has 5 convolutional stages:
1. conv-conv-pool
2. conv-conv-pool
3. conv-conv-pool
4. conv-conv-conv-pool
5. conv-conv-conv-pool
#### Choices
> [!faq]- Why kernel-size 3x3 in conv?
> Two conv of 3x3 has same receptive field as one 5x5
> * Easier to compute
> ![[Pasted image 20241202130503.png]]
> 
> Why use bigger kernel sizes when I can stack 3x3s?

> [!faq]- Why 2x2 stride 2 max pool? Why double the number of channels after pool?
> We want each spatial resolution to take the same amount of computation
> * Half the spatial size
> * Double the number of channels

#### AlexNet vs VGG: Much bigger network!
![[Pasted image 20241202130930.png]]

## GoogLeNet (22 Layers)
##### Focus on Efficiency!
* Reduce parameter count
* Memory usage
* Computation

### Stem network
Aggressively downsamples input
* Usually large computation at the beginning
##### Compare to VGG
![[Pasted image 20241202131447.png]]

### Inception Module
Local unit with parallel branches
**Local structure repeated many times throughout the network**
> [!tldr] No [[Hyperparameters]], just try all kernel sizes
> ![[Pasted image 20241202131653.png]]

### Global Average Pooling
> [!important] No large FC layers at the end!
> Use global average pooling to collapse spatial dimensions, and one linear layer to produce class scores

### Auxiliary Classifiers
##### Problem
Training using loss at the end of the network didn’t work well:
* Network is too deep
* Gradients don’t propagate cleanly
##### Solution (hacky)
Attach ‘auxiliary classifiers’ at several intermediate points in the network that also try to classify image and receive loss

**[[Batch Normalization]] solved this issue**
* Came after GoogLeNet

## Residual Networks
**Once we have [[Batch Normalization]], we can train networks with 10+ layers**
> [!faq] What happens as we go deeper?
> Deeper model does worse than shallow model!
> ![[Pasted image 20241202132333.png]]
> 
> This is an *optimization* problem. Deeper models are harder to optimize, and in particular don’t learn identity functions to emulate shallow models

### Residual blocks
Change the network so learning identity functions with extra layers is easy
![[Pasted image 20241202132633.png]]

> [!tldr] A residual network is a stack of many residual blocks

### Bottleneck Block
![[Pasted image 20241202133130.png]]

**Able to train very deep networks**
**Deeper networks do better than shallow networks**

### Improving ResNets
##### Re-organize blocks
![[Pasted image 20241202133441.png]]

##### Parallel bottleneck blocks (ResNeXt)
![[Pasted image 20241202133753.png]]
> [!important] Maintain computation by adding groups!

## Densely Connected Neural Networks
> [!tldr] Dense blocks where each layer is connected to every other layer in feedforward fashion
> * Alleviates vanishing gradients
> * Strengthens feature propagation
> * Encourages feature reuse

## MobileNets: Tiny Networks
> [!tldr] Maximize efficiency, less accurate

## Neural Architecture Search
**Automating neural architecture creation**
* One network (**controller**) outputs network architectures
* Sample **child networks** from controller and train them
* After training a batch of child networks, make a gradient step on controller network
* Over time, controller learns to output good architectures
> [!warning] VERY EXPENSIVE!!!!



