---
dg-publish: true
tags: cs484
---
# Self-Attention Layer
##### One query per input vector
* We can calculate the query vectors from the input vectors
	* Defining a “self-attention” layer
	* Query vectors are calculated using a FC layer
	* No input query vectors anymore
![[Pasted image 20241202234455.png]]
### Permutation Equivariant
* Self-attention layer doesn’t care about the orders of the input
* Consider permuting the input vectors
	* Outputs will be the same but permuted
#### Positional Encoding
Make processing position-aware
* Concatenate input with **positional encoding**
E can be learned lookup table, or fixed function
![[Pasted image 20241202234939.png]]
### Masked Self-Attention Layer
##### Don’t let vectors “look ahead” in the sequence
* Only use information from the past
Used for language modeling
* predict next word
![[Pasted image 20241202235217.png]]
### Multihead Self-Attention Layer
##### Use $H$ independent “Attention Heads” in parallel
[[Hyperparameters]]
* Query dimension $D_Q$
* Number of heads $H$
![[Pasted image 20241202235357.png]]
### Example: [[Convolutional Neural Networks|CNN]] with Self-Attention
![[Pasted image 20241202235811.png]]
