---
dg-publish: true
---
# Linked Files

> [!tldr] Linked list of data blocks
> * Keep a linked list of all free blocks

![[Pasted image 20231210105944.png]]
### [[Inode]] contents
* pointer to file’s first block
**In each block, keep a pointer to the next block**

### Pros
*  Easy dynamic growth
* No [[fragmentation]]
### Cons
* Non-contiguous blocks cause poor access time
* Poor non-sequential access
* Pointer takes up room in block