---
tags:
  - cs484
dg-publish: true
---
# Nearest Neighbour
### Predict based on most similar images
1. Memorize all data and labels
2. Predict the label of the most similar training image

### Training
* O(1)
* Simply remembers all the training data

### Predict
* Calculate [[L1 Distance]] for each training image
* Predict label of closest image

![[Pasted image 20241129155523.png]]
### Problem
Single nearest neighbor will be affected by outliers
* e.g. yellow area in green

## K-Nearest Neighbors
>[!tldr] Instead of copying from nearest neighbor, take a **majority vote** of **k** closest points

**Never used for images**
* Very slow
* Distance metrics on pixels are not informative
![[Pasted image 20241129163530.png]]

![[Pasted image 20241129160041.png]]

## [[Hyperparameters]]
* What is the best value of **k** to use?
* What is the best **distance** to use?
