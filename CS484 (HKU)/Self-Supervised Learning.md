---
tags:
  - cs484
  - unit
dg-publish: true
---
# Self-Supervised Learning
> [!tldr] Self-supervised learning aims to learn from data without manual label annotations
> * Solve “pretext” tasks that produce good features for downstream tasks
> 	* Learn with supervised learning objectives
> 	* Labels of these pretext tasks are generated *automatically*

#### What is a good feature representation that we want to learn?
* Transferable to different downstream tasks
* Generalizable to different image domains
* We are interested in learning “semantic features”
#### What should be good “pretext tasks” for learning the good features?
* The pretext tasks do not require extra annotations

## Self-supervised pretext tasks
Example: Learn to predict image transformations / complete corrupted images
![[Pasted image 20241206213533.png]]
1. Solving the pretext tasks allow the model to learn good features
2. We can automatically generate labels for the pretext tasks

### How to evaluate a self-supervised learning method?
We usually don’t care about the performance of the self-supervised learning tasks
* We don’t care if the model learns to predict image rotation perfectly
Evaluate the learned feature encoders on downstream target tasks
![[Pasted image 20241206213736.png]]
1. Learn good feature extractors from self-supervised pretext tasks
2. Attach a shallow network on the feature extractor
	1. train the shallow network on the target task with small amount of labeled data

## Pretext Task
### Predict Rotations
**Hypothesis**
A model could recognize the correct rotation of an object only if it has the “visual common-sense” of what the object should look like unperturbed

![[Pasted image 20241206214109.png]]
* Self-supervised learning by rotating the entire input images
* The model learns to predict which rotation is applied
### Predict Relative Patch Locations
![[Pasted image 20241206214242.png]]
### Solving Jigsaw Puzzles
![[Pasted image 20241206214259.png]]
### Predict Missing Pixels (Inpainting)
![[Pasted image 20241206214612.png]]
#### Learning to inpaint by reconstruction
![[Pasted image 20241206214646.png]]
### Learning Features from Colorization: Split-brain Autoencoder
#### Idea: Cross–channel predictions
![[Pasted image 20241206214932.png]]
![[Pasted image 20241206215019.png]]
### Image Coloring
![[Pasted image 20241206215125.png]]
Concatenate (L,ab) channels
![[Pasted image 20241206215209.png]]
### Video Coloring
#### Idea: Model the temporal coherence of colors in videos
![[Pasted image 20241206215255.png]]
**Hypothesis:** Learning to color video frames should allow model to learn to track regions or objects without labels
##### Learning Objective:
Establish mappings between reference and target frames in a learned feature space
Use the mapping as “pointers” to copy the correct color
![[Pasted image 20241206215428.png]]
![[Pasted image 20241206215500.png]]
### Tracking emerges from colorization
#### Propagate segmentation masks using learned attention
![[Pasted image 20241206215617.png]]
#### Propagate pose keypoints using learned attention
![[Pasted image 20241206215641.png]]
### Problem: Learned representations may not be general
![[Pasted image 20241206215748.png]]
## Contrastive Representation Learning
![[Pasted image 20241206215948.png]]
**We want:**
$$\text{score}(f(x), f(x^+)) >> \text{score}(f(x), f(x^-))$$
Given a chosen score function, we aim to learn an **encode function** $f$ that yields high score for positive pairs $(x, x^+)$ and low scored for negative pairs $(x, x^-)$
### A Formulation of contrastive learning
Loss function given 1 positive sample and N-1 negative samples:
![[Pasted image 20241206220437.png]]
Cross entropy loss for a N-way [[Softmax Classifier]]!
* Learn to find the positive sample from the N samples

### SimCLR: A Simple Framework for Contrastive Learning
Cosine similarity as the score function:
![[Pasted image 20241206220626.png]]
Use a projection network $g(\cdot)$ to project features to a space where contrastive learning is applied
![[Pasted image 20241206220739.png]]
Generate positive sample through data augmentation:
* Random cropping, random color distortion, and random blur
* e.g. positive samples
![[Pasted image 20241206220846.png]]
### Mini-batch Training
![[Pasted image 20241206220923.png]]
### Design Choices
#### projection head
Linear / non-linear projection heads improve representation learning
![[Pasted image 20241206221040.png]]
* By leveraging the projection head $g(\cdot)$, more information can be preserved in the $h$ representation space
#### Large batch size
![[Pasted image 20241206221150.png]]
## Momentum Contrastive Learning (MoCo)
##### Motivation
* Self-supervised learning can be thought of as building dynamic dictionaries. An encoded “query” should be similar to its matching key and dissimilar to others
* Dictionaries should be **large** (large number of negative samples better sample the underlying continuous, high dimensional visual space) and **consistent** (keys in the dictionary should be represented by the same or similar encoder so that their comparisons to the query are consistent)
![[Pasted image 20241206221818.png]]
#### Key differences to SimCLR
* Keep a running queue of keys
* Compute gradients and update the encoder only through the queries
* Decouple min-batch size with the number of keys
	* Can support a large number of negative samples
* The key encoder is slowly progressing through the momentum update rules
	* $\theta_k ← m\theta_k + (1-m)\theta_q$
![[Pasted image 20241206222148.png]]
### MoCo V2
A hybrid of ideas from SimCLR and MoCo:
**From SimCLR:** Non-linear projection head and strong data augmentation
**From MoCo:** Momentum-updated queues that allow training on a large number of negative samples

## Masked Autoencoder
**Idea:** 
1. Mask some patches
2. Predict masked patches
![[Pasted image 20241206222524.png]]

**Random masking up to 75% of patches:**
* Random mask avoids center bias
* Create challenging pre-task for model to learn the image semantics
* Efficient computation![[Pasted image 20241206222652.png]]

**Encoding Visible Patches:**
* Encoder: Vision [[Transformers]] (ViT)
* Linear projection for mapping pixel values to patch embeddings
* Positional embeddings are added to the patch embeddings![[Pasted image 20241206222747.png]]

**Decoding Masked Patches**
* Decoder: ViT
* Decoders makes prediction based on
	* Visible patches
	* Masked tokens
* Position embeddings are added to all patches
* 16 x 16 pixels = a 256-dim vector
* MSE for loss training![[Pasted image 20241206233522.png]]
The decoder is throwed after pre-training and full patches are encoded during downstream fine-tuning

