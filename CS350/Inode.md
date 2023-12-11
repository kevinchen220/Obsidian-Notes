# Inode
> [!tldr] Structure tracking a file’s sectors is called an index node

## Overview
Inodes are stored in fixed-size array
* The size of the array is fixed when the disk is initialized and cannot be changed
* It lived in known location
* Metadata is smeared across it
	* For indirect and double indirect blocks
* Index of an inode in the inode array is an **i-number**
	* OS refers to files by **i-number**
* When file is open, inode is brought into memory
* Inode is written back when file is modified
**Inode maps a file offset → a data block for its file**
* contains metadata about the file
	* Permissions
	* Access/modification/change time
	* link count


> [!question] How is a new inode allocated?
> Each file requires a new inode
> * If it is a new file, put in same [[cylinder group]] as directory
> * If it is a new directory, use a different cylinder group

