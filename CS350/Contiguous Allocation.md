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