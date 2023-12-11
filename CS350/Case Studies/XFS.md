# XFS

> [!tldr] Think big
> Big disks, big files, large number of files, 64-bit everything
> * Still maintain very good performance

Break disk up into [[Allocation Groups]] (AGs)
* New directories go in new AGs
* Within directory, inodes of files go in same AG
* Unlike [[cylinder group]], **AGs too large to minimize seek time**
* Also no fixed number of [[inode]] per AG

**XFS makes extensive use of [[B+ Trees]]**
## B+ trees in XFS
* Directories
	* Make large directories efficient
* Inodes to block pointers
	* B+ tree maps: file offset → (start block, # blocks)
* i-number to inode
	* High bits of i-number specify allocation group
	* B+ tree in AG maps: starting i-number → (block #, free-map)
* Free extents tracked by two B+ trees
	1. start block # → # free blocks
	2. # free blocks → start block # 
Use [[journaling]] to update both atomically and consistently
