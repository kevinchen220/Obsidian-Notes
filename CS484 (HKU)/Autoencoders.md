---
tags: cs484
dg-publish: true
---
# Autoencoders
Unsupervised approach for learning feature vectors from raw data x, without any labels
* Features should extract useful information that we can use for downstream tasks

#### How can we learn this feature transform from raw data?
Use the features to **reconstruct** the input data with a **decoder**
* “Autoencoding” = encoding itself
**Loss:** [[L2 Distance]] between input and reconstructed data
![[Pasted image 20241205161531.png]]
> [!tldr] Want features to be **lower dimensional** than data
> Compress input data

After training, **throw away decoder** and use encode for a downstream task
![[Pasted image 20241205161914.png]]

Autoencoders can reconstruct data, and can learn features to initialize a supervised model
Features capture factors of variation in training data
*We can’t generate new images from an autoencoder because we don’t know the space of z*
