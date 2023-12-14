---
dg-publish: true
---
# Block Allocation
## Goal
Optimize for sequential access
* If available, use rotationally close block in same cylinder
* Otherwise, use block in same [[cylinder group]]
* If CG full, find another CG with quadratic hashing
	* If CG n is full, try $n+1^2, n+2^2, n+3^2,...$
* Else use any CG

### Problem
**Don’t want large files filling up whole CG**
* Otherwise other [[inode]] will not have room for their data
### Solution
**Break large files over many CGs**
* Still need to have large extents in each CG
	* So sequential access is still quick

> [!question] How big should the extents be?
> Extent transfer time should be much greater than seek time
