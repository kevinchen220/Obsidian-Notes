---
tags:
  - unit
---
# File Systems
> [!NOTE] Main Goal of file systems
> * **Don’t go away**: From boot up to shut down
> * Associate bytes with name (files)
> * Associate names with each other (directories)

## [[Secondary storage]]
## [[Files]]
## File systems vs. [[Virtual Memory]]
* Both aim to have **location transparency**
	* The ability to access data without knowing the location
#### FS has an easier job than VM
* Using processor time for FS mappings is ok
	* No [[TLB]]
	* FS access is less frequent
	* Files are dense, more sequential
#### FS is harder
* A lot of space
* File size range is extreme
## [[Performance of File Systems]]
## Common patterns
* Sequential
	* File data is often processed in sequential order
* Random access
	* Address any block in file directly without passing through predecessors
	* e.g. databases
* Keyed access
	* Search for block with particular value

## How to track all file’s data?
* File system management
	* Need to keep track of where files are in secondary storage
	* Must be able to use this to map byte offset to data block
	* [[Inode]] must be stored within the file system too
* Thing to keep in mind
	* Most files are small
	* Much of the disk is allocated to large files
	* Many of the I/O operations are made to large files
### Attempt 1: [[Contiguous Allocation]]
### Attempt 2: [[Linked Files]]
### Attempt 3: [[FAT]]