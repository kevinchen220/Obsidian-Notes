---
tags:
  - unit
  - cs484
dg-publish: true
---
# Image Classifier
> [!note] There is no obvious way
> Cannot hard code an algorithm

### Attempts
Find edges and corners
* Categorize edges and boundaries
* Not scalable for multiple categories

### Data-Driven Approach
1. Collect a dataset of images and labels
2. Use Machine Learning to train a classifier
3. Evaluate the classifier on new images

```python
def train(images, labels):
	# Machine Learning!
	return model

def predict(model, test_images):
	# Use model to predict labels
	return test_labels
```

## How do we compare images?
#### [[L1 Distance]]
#### [[L2 Distance]]


## [[Hyperparameters]]

## Different Classifiers

> [!important] We want fast predictions
> More practical when put in use
> * Want low latency
> 
> Slow training is fine
> * Can be done in the background
### [[Nearest Neighbour]]

### [[Linear Classification]]

### [[Softmax Classifier]]

## Use [[Loss Functions & Optimizations]] to determine how good the classifier is
> [!todo]
> 1. Define a **loss function** that quantifies our unhappiness with the scores across the training data
> 2. Come up with a way of efficiently finding the parameters that minimize the loss function (**optimization**)


