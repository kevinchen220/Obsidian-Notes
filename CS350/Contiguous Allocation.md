---
dg-publish: true
---
# Contiguous Allocation

> [!tldr] Allocate files like segmented memory
> When creating a file, make the user pre-specify the length and allocate all at once

![[Pasted image 20231210105731.png]]
### [[Inode]] contents
* location and size
#### Pros
* simple
* fast
Cons
* [[Fragmentation#External Fragmentation|External Fragmentation]]


> [!question] How do you know how large a file will be?
> Use **Delayed Allocation**
> * The `write` syscall only affects the buffer cache
> * Allow write into buffers before deciding where to place it on disk
> * **Assign disk space only when the buffers are flushed**
#### Other advantages
* Short-lived files never need disk space allocated
* Write clustering
	* Find other nearby stuff to write to disk
