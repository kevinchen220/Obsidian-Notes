---
tags:
  - cs484
  - unit
dg-publish: true
---
# Videos
> [!tldr] 2D + Time
> A video is a sequence of images

##### 4D tensor: T x 3 x H x W

## Video Classification
Fixed size of categories like [[Image Classification]]
![[Pasted image 20241205222025.png]]
In video classification, we want to recognize actions

### Problem: Videos are big!
Videos are ~30 frames per second
Size of uncompressed video (3 bytes per pixel)":
* SD (640 x 480): ~1.5 GB per minute
* HD (1920 x 1080): ~10 GB per minute
> [!success] Train on short clips
> * Low fps
> * Low spatial resolution
> 	* e.g. T=16, H=W=112
> 		* 3.2 seconds at 5 fps, 588KB

![[Pasted image 20241205222656.png]]
#### Testing
**Run model on different clips, average predictions**
![[Pasted image 20241205222920.png]]
## Single-Frame [[Convolutional Neural Networks|CNN]]
#### Idea
Train normal 2D CNN to classify each video frames independently!
* Average predicted probs at test-time
Often a very strong baseline for video classification
![[Pasted image 20241205223132.png]]
## Late Fusion
#### Intuition
Get high-level appearance of each frame and combine them
### With FC Layers
![[Pasted image 20241205223143.png]]
### With Pooling
Less learnable parameters compared to FC
![[Pasted image 20241205223310.png]]
> [!warning] Hard to compare low-level motion between frames

## Early Fusion
#### Intuition
Compare frames with very first conv layer
* after that normal 2D CNN
*First 2D convolution collapses all temporal information*
![[Pasted image 20241205223624.png]]
> [!warning] One layer of temporal processing may not be enough

## 3D CNN (Slow Fusion)
#### Intuition
Use 3D versions of convolution and pooling to slowly fuse temporal information over the course of the network
![[Pasted image 20241205223824.png]]

## Early Fusion vs Late Fusion vs 3D CNN
#### Late Fusion
* Build slowly in space
* All-at-once in time at end
![[Pasted image 20241205224011.png]]
#### Early Fusion
* Build slowly in space
* All-at-once in time at start
#### 3D CNN
* Build slowly in space
* Build slowly in time
![[Pasted image 20241205224145.png]]

### Accuracy
![[Pasted image 20241205224816.png]]
## 2D Conv vs 3D Conv
![[Pasted image 20241205224525.png]]
![[Pasted image 20241205224538.png]]

## C3D: The [[CNN Architectures#VGG (19 Layers)|VGG]] of 3D CNNs
3D CNN that uses all 3x3x3 conv and 2x2x2 pooling
* Except Pool1 with 1x2x2
![[Pasted image 20241205232321.png]]
> [!warning] 3x3x3 conv is very expensive!
> * AlexNet: 0.7GFLOP
> * VGG-16: 13.6 GFLOP
> * C3D: **39.5 GFLOP**

![[Pasted image 20241205232514.png]]
> [!faq] Maybe we should treat space and time separately?

## Measuring Motion: Optical Flow
Optical flow gives a displacement field F between images $I_t$ and $I_{t+1}$
* Tell where each pixel will move in the next frame
* Vertical and horizontal flow
![[Pasted image 20241206141542.png]]
### Two-Stream Networks
Separating Motion and Appearance
* Top stream processes appearance of input video
* Lower stream is motion stream
	* Processing only motion
![[Pasted image 20241206141729.png]]
#### Performance
![[Pasted image 20241206141914.png]]
## Modeling long-term temporal structure
>[!faq] So far, all our temporal CNNs only model local motion between frames in very short clips. What about long-term structure?
> We can handle sequences with [[Recurrent Neural Networks]]!

Inside CNN: Each value is a function of a fixed temporal window
Inside RNN: Each vector is a function of all previous vectors
![[Pasted image 20241206142313.png]]
>[!faq] Can we merge both approaches?

### Recurrent Convolutional Network
![[Pasted image 20241206142355.png]]
![[Pasted image 20241206142440.png]]

> [!warning] RNNs are slow for long sequences
> RNNs cannot be parallelized

### [[Self-Attention Layer|Self-Attention]]
![[Pasted image 20241206145445.png]]
> [!faq] Where should we add this block?

### Inflating 2D Networks to 3D (I3D)
##### Idea
Take a 2D CNN architecture
* Replace each 2D $K_h \times K_w$ conv/pool layer with a 3D $K_t\times K_h\times K_w$ version
##### Original
![[Pasted image 20241206145836.png]]
##### Updated
![[Pasted image 20241206145857.png]]

#### Transfer Weights
Can use weights to 2D conv to initialize 3D conv
* Copy $K_t$ times in space and divide by $K_t$
* This gives the same result as 2D conv given “constant” video input
![[Pasted image 20241206150045.png]]
##### Performance
![[Pasted image 20241206150453.png]]

## Vision [[Transformers]] for Video
![[Pasted image 20241206150858.png]]
