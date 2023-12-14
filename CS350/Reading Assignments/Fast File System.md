---
dg-publish: true
---
# Fast [[File Systems]]
## Goals
* Enhancing performance
* Reducing fragmentation
* Improving reliability
* Supporting larger file systems
### Improvements and Innovations
Block size optimization
* Larger block sizes
* Reduce overhead of managing file metadata

Cylinder groups
* Organizing disk blocks into [[cylinder]] groups to improve locality and reduce seek times
* Made of one or more consecutive cylinders on a [[disk]]

Metadata Optimization
* Using a more efficient format for storing metadata like inodes and directories
* Leading to faster access and reduced overhead

**Keep [[inode]] close to data blocks**
**Try to allocate consecutive inodes for files in same directory**
**Each cylinder group had its own bitmap for available blocks**
**Bookkeeping information stored scattered so that it will not all be lost**

