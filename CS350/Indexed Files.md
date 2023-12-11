# Indexed Files

> [!tldr] Each file has an array holding all of it’s block pointers
> Similar to page table
> * Max file size fixed by array’s size
> * Allocate array to hold file’s block pointers during file creation
> * Allocate actual blocks on demand using free list
> ![[Pasted image 20231210144552.png]]

### Pros
* Both sequential and random access are easy
### Cons
* Mapping table requires large chunk of contiguous space
#### Solution?
Multilevel page tables
* Small regions with index array
**downside**
* More FS accesses
* Expensive
![[Pasted image 20231210144734.png]]


