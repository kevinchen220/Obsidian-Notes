# Speeding up FS
### Original file system design
![[Pasted image 20231210153921.png]]
Components:
* Data blocks
	* Contain the file data
* [[Inode]]
	* Contain meta information about the file
* [[Hard Links]]
* [[Superblock]]
	* Specifies information about the file system
#### Problems
**SLOW**
* Blocks too small
	* 512 bytes
	* Transfer rate slow
* Poor clustering of related objects
	* Consecutive blocks not close together
	* Inodes far from data blocks
	* Inodes for directory not close together
	* Poor enumeration performance
		* e.g. `ls`, `grep foo *.c`
**[[Fragmentation#Internal Fragmentation|Internal Fragmentation]]**
> [!question] Why not just make block size bigger?
> * Bigger block size increase bandwidth but also increase internal fragmentation

> [!success] Solution
> Have larger block sizes
> * Also allow large blocks to be chopped in to smaller ones

### Clustering Related Objects
Group one or more consecutive cylinders into [[cylinder group]]
![[Pasted image 20231210155526.png]]
**Key Idea**
* The system can access any block in a cylinder without performing a seek
	* Next fastest place is an adjacent cylinder
* Try to put sequential blocks together
*![[Pasted image 20231210155714.png]]
* Try to keep inode and file data together
![[Pasted image 20231210155724.png]]

> [!question] What does our disk layout look like now?
> **Each cylinder group is basically a mini file system**
> ![[Pasted image 20231210155906.png]]
> Bookkeeping information
> * Block bitmap
> 	* Bitmap of available fragments
> * Summary info within each cylinder group
> 	* if free inodes, blocks, fragments

### Finding space for related objects
**Old Unix**
* Maintained a linked list of free data blocks
* Need another data block → remove one from the head of the list
**FFS**
* Bitmap of free blocks
* Easier to find contiguous blocks
* Small
### Using a bitmap
**Keep entire bitmap in memory**
> [!tip] Calculate bitmap size
> bitmap size = disk size / block size / 8

> [!question] How do we allocate a block close to block x?
> Check for blocks near x / array element size

### What did we gain?
Performance improvements
* 20-40% of disk bandwidth for large files
* 10-20x faster than original system
We can do better with **[[Extent Based]]** system
* Named contiguous blocks with single pointer and length