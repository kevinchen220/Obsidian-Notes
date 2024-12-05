---
dg-publish: true
tags:
  - cs484
  - unit
---
# Instance Segmentation
>[!tldr] Combination of [[Semantic Segmentation]] and [[Object Detection]]
>Detect all objects in the image, and identify the pixels that belong to each
>* Only **things** not **stuff**
>	* Objects that can be separated into object instances

> [!example] Approach
> 1. perform object detection
> 2. predict a segmentation mask for each object

## Mask R-CNN
*Adding onto [[Object Detection#Faster R-CNN]]*
### Attach a separate branch for segmentation
![[Pasted image 20241205134806.png]]
![[Pasted image 20241205134834.png]]
#### Example Training Targets
A pair of boundary box, category and segmentation mask
![[Pasted image 20241205135000.png]]
## Panoptic Segmentation
Label all pixels in the image
* Both things and stuff

## Keypoint Estimation
![[Pasted image 20241205135209.png]]
Attach another branch on Mask R-CNN
![[Pasted image 20241205135233.png]]
### We can attach different branches to achieve different final results

