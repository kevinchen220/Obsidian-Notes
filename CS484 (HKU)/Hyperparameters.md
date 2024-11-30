---
tags: cs484
dg-publish: true
---
# Hyperparameters
> [!tldr] Choices about the algorithm that we set rather than learn

Very problem dependent
Must try them all out to see what works best

### Setting Hyperparameters
#### Idea 1: Choose hyperparameters that work best on the data
> [!warning] BAD: K=1 always works perfectly on training data

![[Pasted image 20241129163216.png]]
#### Idea 2: Split data into train and test
Choose hyperparameters that work best on test data
> [!warning] BAD: No idea how algorithm will perform on new data

![[Pasted image 20241129163228.png]]
#### Idea 3: Split data into train, val, and test
Choose hyperparameters on **val** and evaluate on **test**
> [!success] Better!

![[Pasted image 20241129163241.png]]

> [!danger] Do not want to touch test set until actual testing

#### Idea 4: Cross-Validation
Split data into **folds**, try each fold as validation and average the results
* Useful for small datasets, but not used too frequently in deep learning
![[Pasted image 20241129163142.png]]