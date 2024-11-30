---
tags:
  - cs484
  - unit
dg-publish: true
---
# Image Classification
### What a computer sees
A grid of numbers between [0, 255] RGB values
* e.g. 800 x 600 x 3 (three channels for RGB)

> [!tldr] Semantic Gap
> What we see is different from what a computer sees
> * Only pixel values

### Challenges
#### Viewpoint Variation
* all pixels change when the camera moves
#### Illumination
* Different lighting conditions affect the pixel values
#### Deformation
* Different poses and positions
#### Occlusion
* Only see parts of an object
#### Background Clutter
* Object similar to background
#### Intraclass Variation
* Object may have various subcategories
* e.g. different breeds of cats

## [[Image Classifier]]

### Previously
**Feature Extraction**
Examples
* Color Histogram
* Histogram of oriented gradients
* Bag of words
