---
tags:
  - cs484
  - unit
---
# Vision and Language
### Why Vision + Language?
* We live in a multi-modal world
* We learn from both vision and language modalities
* **Allows AI to interact with human beings**
* Language provides **open–set and comprehensive semantic information** for visual perception![[Pasted image 20241207001137.png]]
## Vision-language Joint Embedding
#### What is a vision-language joint embedding space?
![[Pasted image 20241207001251.png]]
#### Why vision-language joint embedding?
1. Enrich training samples & labels for visual recognition model
	1. **Samples:** annotated images are considerably limited VS. image-text pairs
	2. **Labels:** Generalizing to unseen object categories
2. Image-text / text-image retrieval
3. Useful for downstream vision-language tasks
#### How is Vision-Language Joint Embedding Learned?
* Data: image-text pairs
* Joint embedding: Alignment!
![[Pasted image 20241207001715.png]]
## CLIP
>[!success] Rather than needing handcrafted labels to train a good classifier for a given domain, we can leverage free-form text from the internet to learn a model that is a good classifier for all domains
#### Training
* CLIP is trained to classify which text caption in a batch corresponds to each image in a batch
![[Pasted image 20241207001921.png]]
#### Inference
* Create new zero-shot classifiers during inference:
	* fetch the text embeddings for a set of classification labels
	* compute these labels’ similarity to a given image
![[Pasted image 20241207001926.png]]

#### Evaluation and Applications
* Calculate image-text similarities
* Image-text retrieval based on image-text similarities
* Image classification
* Representation learning

## ImageBind
### Bridging More Modalities
* One embedding space to bind all modalities
## Image Captioning
* Describe the content of an image or video with a natural language sentence
#### Encoder-decoder structure
![[Pasted image 20241207002458.png]]
* Visual Encoders![[Pasted image 20241207003109.png]]
* Visual Decoders![[Pasted image 20241207003121.png]]
* Show and Tell
	* Encode the image with a CNN-based model
	* Decode the image in an autoregressive fashion using an RNN (LSTM) language model
![[Pasted image 20241207002816.png]]

* Bottom-up and Top-down attention
	* Usually models operate on CNN features corresponding to a uniform grid
	* What if we use features from object detections instead?
![[Pasted image 20241207003310.png]]
## Video Captioning
* Video to text (sequence to sequence)
![[Pasted image 20241207002725.png]]
## Scene graph
Scene graph is a structured way to represent information from images
![[Pasted image 20241207003339.png]]
## Visual Question Answering
Answering open-ended questions about images which require an understanding of vision, language,  and common sense knowledge
### VQA as image + text → text
![[Pasted image 20241207003528.png]]
### VQA as classification
![[Pasted image 20241207003556.png]]
### Bottom-up and top-down attention
![[Pasted image 20241207003643.png]]
## Visual Grounding
Locate relevant objects in the image
![[Pasted image 20241207003741.png]]