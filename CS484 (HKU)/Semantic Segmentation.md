---
dg-publish: true
tags:
  - cs484
  - unit
---
# Semantic Segmentation
> [!tldr] Label each pixel in the image with a category label
> Does not differentiate between different instances

![[Pasted image 20241205132015.png]]\
## Sliding Window
For every pixel, create a small patch
→ Send patch to CNN to classify pixel

## Fully Convolutional Network
Design a network as a bunch of convolutional layers to make predictions for pixels all at once
![[Pasted image 20241205132302.png]]
> [!warning] Expensive!

>[!success] Design network as a bunch of convolutional layers, with **downsampling** and **upsampling** inside the network
![[Pasted image 20241204143752.png]]

### Upsampling (Unpooling)
#### Bed of Nails
Fill with 0s
![[Pasted image 20241205132604.png]]
#### Nearest Neighbor
Copy nearest neighbor
![[Pasted image 20241205132636.png]]
#### Bilinear Interpolation
Use two closest neighbors in x and y to construct linear approximations
![[Pasted image 20241205132731.png]]
#### Bicubic Interpolation
Use three closest neighbors in x and y to construct cubic approximations
* This is how we normally resize images!
![[Pasted image 20241205132930.png]]
#### Max Unpooling
Pair each max pooling layer with a max unpooling layer
* Remember which position had the max
* Place each max into remembered positions
* Fill rest with 0s
![[Pasted image 20241205133152.png]]
### Learnable Upsampling: Transposed Convolution
![[Pasted image 20241205133744.png]]
#### 1D Example
![[Pasted image 20241205133813.png]]
