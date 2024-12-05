---
dg-publish: true
tags:
  - cs484
  - unit
---
# Recurrent Neural Networks
### So far: “Feedforward” Neural Networks
![[Pasted image 20241202210814.png]]
> [!faq]- What if we want other types of networks
> What about one to man?
> ![[Pasted image 20241202210846.png]]
> What about many to one?
> ![[Pasted image 20241202210859.png]]
> What about many to many?
> ![[Pasted image 20241202211028.png]]
> * Machine translation: sequence of words → sequence of words

## Key Idea
> [!important] RNNs have an “internal state” that is updated as a sequence is processed
> We can process a sequence of vectors **x** by applying a **recurrence formula** at every time step:
> $$h_t = f_w(h_{t-1}, x_t)$$
> $h_t$ = new state
> $f_w$ = some function with parameters $W$
> $h_{t-1}$ = old state
> $x_t$ = input vector at some time step

### Vanilla Recurrent Neural Networks
![[Pasted image 20241202213640.png]]

$$h_t = \tanh(W_{hh}h_{t-1}+W_{xh}x_t)$$
$$y_t = W_{hy}h_t$$
## RNN Computational Graph
Initial hidden state
* Either set to all 0
* Or learn it
>[!important] Re-use the same weight matrix at every time-step

> [!faq] What of different timesteps have different weights?
> * Can only predict fixed input length
> 	* depends on number of weight matrices
> * Model size increase linearly with number of timesteps
> * Different weights applied on different timesteps
> 	* difficult to learn weights

![[Pasted image 20241202213955.png]]

#### Many to Many
![[Pasted image 20241202214152.png]]
#### Many to One
![[Pasted image 20241202214315.png]]
#### One to Many
![[Pasted image 20241202214328.png]]
#### Sequence to Sequence (Machine translation)
**Many to One + One to Many**
* Encoder + Decoder
![[Pasted image 20241202214427.png]]
>[!example]- Example: Language Modeling
>Given characters 1, 2, …, t, model predicts character t
>* Predicts at each time-step
>![[Pasted image 20241202214645.png]]

At test-time, **generate** new text:
* sample characters one at a time
* feed back to model
![[Pasted image 20241202214823.png]]
> [!important]- So far: encode inputs as **one-hot-vector**
> ![[Pasted image 20241202215027.png]]
> Matrix multiply with a one-hot-vector just extracts a column
> * Often extract this into a separate **embedding layer**
>![[Pasted image 20241202215033.png]]

## [[Backpropagation]] Through Time
![[Pasted image 20241202215127.png]]
> [!warning] Take a lot of memory for long sequences!

#### Truncated Backpropagation Through Time
![[Pasted image 20241202215355.png]]
> [!tldr]
> Run forward and backward through **chunks of the sequence** instead of whole sequence
> 
> Carry hidden states forward in time forever, but only backpropagate for some smaller number of steps

## RNN Tradeoffs
Advantages
* Same weights applied on every timestep
* Can process any length input
* Computation for step t can use information from many steps back
* Model size doesn’t increase for longer input
Disadvantages
* Recurrent computation is slow
* In practice, difficult to access information from many steps back
## Example: Image Captioning
![[Pasted image 20241202220712.png]]
1. Take feature vector coming out of [[Convolutional Neural Networks|CNN]]
2. Feed into RNN
![[Pasted image 20241202221808.png]]
Result:
![[Pasted image 20241202221913.png]]
>[!important] We have a **START** token for the beginning of the predict and an **END** token to know when to end

