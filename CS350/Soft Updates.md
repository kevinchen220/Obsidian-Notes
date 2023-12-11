# Soft Updates
## Goal
**Want to avoid crashing after “bad” subset of writes**
Must follow 3 rules in ordering updates
1. Never write pointer before initializing the structure it points to
2. Never reuse a resource before nullifying all pointers to it
3. Never clear last pointer to live resource before setting new one

> [!example] Create file A
> Block X contains inode
> Block Y contains directory block
> Task: create file A in inode block X and directory Y
> We say Y→ X, meaning Y depends on X
> * X is **dependee**, Y is **depender**
## More problems
Crash might occur between ordered but related writes
* Summary information wrong after block freed
Block aging
* Block that always has dependency will never get written back

### Solution
Write blocks in any order
* Keep track of dependencies
When writing a block
* **Temporarily roll back any changes that cannot be committed yet**
	* Cannot write block with any arrows pointing to dependees
* Then we have no more dependencies and can write a second time
#### In-depth structure
The structure for each updated field or pointer contains:
* old value
* new value
* list of updates on which this update depends on (**dependee**)
System can write the blocks in any order
* Must temporarily roll back updates with pending dependencies
	* ==Must lock rolled-back version so applications don’t see it==
* Some dependencies better handled by postponing in-memory updates

## Operations requiring soft updates
1. Block allocation: **block pointer → free block bitmap, data block**
2. Block deallocation: **free block bitmap → block pointer**
3. Link addition: **directory entry → bitmap, inode**
4. Link removal: **bitmap, inode → directory entry**

## Issues
