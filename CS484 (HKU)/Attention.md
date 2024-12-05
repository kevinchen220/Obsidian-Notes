---
dg-publish: true
tags:
  - cs484
  - unit
---
# Attention
### Problem: Sequence to Sequence (Translation)
![[Pasted image 20241202225036.png]]
> [!faq] Input sequence bottlenecked through fixed-sized vector. What if T = 1000?
> **Idea:**
> * Use new context vector at each step of decoder
> * Use **attention**
> 	1. Compute (scalar) **alignment scores**
> 		* $e_{t,i} = f_{att}(s_{t-1}, h_i)$ ($f_{att}$ is an MLP)
> 	2. Normalize alignment scores to get **attention weights**
> 		* $0<a_{t,i}<1$, $\sum_i a_{t,i} = 0$
> 		* [[Softmax Classifier|Softmax]]
> 	1. Compute context vector as linear combination of hidden states
> 		* $c_t = \sum_i a_{t,i}h_i$
> 	2. Use context vector in decoder
> 		* $s_t = g_u(y_{t-1}, h{t-1}, c_t)$
> 
> ![[Pasted image 20241202225741.png]]
> ### Timestep = 2
> ![[Pasted image 20241202225925.png]]

> [!tldr] Use a different context vector in each timestep of decoder
> * Input sequence not bottlenecked through single vector
> * At each timestep of decoder, context vector “looks at” different parts of the input sequence

## Image Captioning with [[Recurrent Neural Networks|RNNs]] and Attention
### Problem
Input: Image
Output: Sequence $y = y_1, y_2, …, y_t$ (caption)

### Steps
1. Extract spatial features form a pretrained [[Convolutional Neural Networks|CNN]]
2. Compute alignment scores
3. Normalize alignment scores to get attention weights
	1.  [[Softmax Classifier|Softmax]]
4. Compute context vector as linear combination of hidden states
5. Use context vector in decoder
#### Timestep = 1
![[Pasted image 20241202231047.png]]
#### Timestep = 2
![[Pasted image 20241202231117.png]]
#### Timestep = 4
![[Pasted image 20241202231146.png]]


## General Attention Layer
#### Inputs
**Query vector:** q (Shape $D_Q$)
**Input vectors:** X (Shape: $N_x \times D_x$)
**Similarity function:** $f_{att}$
#### Computation
**Alignment:** $e_i = f_{att}(q,x_i)$ (Shape: $N_x$)
**Attention:** $a= \text{softmax}(e)$ (Shape: $N_x$)
**Output:** $c = \sum_ia_ix_i$ (Shape: $D_x$)
#### Outputs
**Context vector:** c (Shape $D_c$)
### Changes for generalization
* Use scaled dot product for alignment
	* Large similarities will cause softmax to saturate and give vanishing gradients
	* Divide by $\sqrt{D}$ to reduce effect of large magnitude vectors
* Multiple **query vectors**
* Separate **key** and **value**
![[Pasted image 20241202234223.png]]

## [[Self-Attention Layer]]

