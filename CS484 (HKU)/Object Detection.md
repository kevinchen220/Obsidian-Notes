---
dg-publish: true
tags:
  - cs484
  - unit
---
# Object Detection
### Type of Computer Vision Tasks
##### Classification
![[Pasted image 20241204143104.png]]
##### Object Detection & Instance Detection
![[Pasted image 20241204143147.png]]

## Object Detection
**Input**: Single RGB Image
**Output**: A *set* of detected objects;
* For each object predict:
	* **Category label** (From fixed, known set of categories)
	* **Bounding Box** (Four numbers: x, y ,width, height)

### Challenges
**Multiple outputs:** Need to output variable numbers of objects per image
**Multiple types of output:** Need to predict category label and bounding box
**Large images:** Classification works at 224x224
* Need higher resolution for detection

### Detecting a **single object**
##### Classification + Localization
Two branches
* Multiple loss functions
* Combine since we only want one loss function for [[Gradient Descent]]
![[Pasted image 20241204153404.png]]
### Detecting **multiple images**
*Need different numbers of outputs per image*
#### Sliding Window
Apply a [[Convolutional Neural Networks|CNN]] to many different crops of the image
* CNN classifies each crop as object or background

> [!warning] Need to apply CNN to huge number of locations, scales, and aspect ratios
> **Very computationally expensive**

#### Region Proposals: Selective Search
* Find small set of boxes that are likely to cover all the objects
	* “blobby” image regions
* Relatively fast to run
	* Gives 2000 region proposal in a few seconds on CPU

## R-CNN: Region-Based CNN
### Steps
1. Run region proposals
	* Get regions of interest
2. For each region proposals
	1. Warp region to fix size
	2. Run independently through CNN
	3. Classify each region
	4. Bounding box regression
![[Pasted image 20241204154226.png]]
### Test time
Input: Single RGB image
1. Run region proposal method to compute ~2000 region proposals
2. Resize each region to 224x224 and run independently through CNN to predict class scores and boundary box transform
3. Use scores to select a subset of region proposals to output
4. Compare with ground-truth boxes

### Comparing Boxes: Intersection over Union
How can we compare out prediction to the ground-truth box?
$$\frac{\text{Area of Intersection}}{\text{Area of Union}}$$
**IoU > 0.5 is “decent”**
**IoU > 0.7 is “pretty good”**
**IoU > 0.9 is “almost perfect”**
![[Pasted image 20241204160219.png]]

### Overlapping Boxes: Non-Max Suppression (NMS)
**Problem:** Object detectors often output many overlapping detections
![[Pasted image 20241204160451.png]]
**Solution:** Post-process raw detections using **NMS**
1. Select next highest-scoring box
2. Eliminate lower-scoring boxes with IoU > threshold (e.g. 0.7)
3. If any boxes remain, go to step 1

>[!warning] NMS may eliminate “good” boxes when objects are highly overlapping…
>![[Pasted image 20241204160657.png]]


## Fast R-CNN

### Problem with Slow R-CNN
#### Very Slow! Need to do ~2k forwards passes for each image!
> [!success] Run CNN **before** warping
> Swap the order
> ![[Pasted image 20241204160918.png]]

![[Pasted image 20241204220728.png]]
Faster because it can share computation between image proposal regions
* **Swapped CNN with cropping + warping**
### What does crop features mean?
#### Region of Interest Pooling
 1. Project proposal onto features
 2. “Snap” to grid cells
 3. Max pool within each subregion

![[Pasted image 20241204221055.png]]
##### Problem
Misalignment when we **snap** to grid cells
#### RoI Align
No “snapping”
![[Pasted image 20241204221237.png]]

### Speed Improvement
![[Pasted image 20241204221555.png]]
> [!warning] Inference is dominated by region proposals
> We should use CNN!!!

## Faster R-CNN
Insert **Region Proposal Network** to predict proposals from features
Otherwise same as Fast R-CNN
* Crop features for each proposal
* Classify each one
![[Pasted image 20241204222023.png]]

### Region Proposal Network
1. Run backbone CNN to get features aligned to input image
2. Image an anchor box of fixed size at each point in the feature map
3. At each point, predict whether the corresponding anchor contains an object
	1. For positive boxes, also predict a box transform to regress from *anchor box* to *object box*
![[Pasted image 20241204222858.png]]
> [!important] Use **K** different anchor boxes at each point
> We want to use anchor boxes of different sizes and shapes

##### Jointly train with 4 losses
1. **RPN Classification:** Anchor box is object / not object
2. **RPN Regression:** predict transform from anchor box to proposal box
3. **Object Classification:** Classify proposals as background / object
4. **Object Regression:** Predict transform from proposal box to object box
![[Pasted image 20241204223249.png]]
#### SPEEDDDDD
![[Pasted image 20241204223304.png]]
### Two-stage Object Detector
First stage: Run once per image
* Backbone network
* Region proposal network
Second stage: Run once per region
* Crop features: RoI pool / align
* Predict object class
* Prediction bbox offset
![[Pasted image 20241204223518.png]]
##### Do we need the second stage?
### Single-Stage Object Detection
![[Pasted image 20241204223952.png]]
![[Pasted image 20241204223620.png]]

Two stage more accurate but slow
Single stage faster but not as accurate
