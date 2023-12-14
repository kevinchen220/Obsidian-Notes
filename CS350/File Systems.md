---
tags:
  - unit
  - cs350
dg-publish: true
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
### Attempt 4: [[Indexed Files]]
### Attempt 5: [[Multi-level Indexed Files]]

## [[Directories]]

## Naming Magic

> [!question] Where do you start looking for a file
> * Root directory always **inode #2**
> 	* Inodes 1 and 2 are reserved for bad blocks
#### Special names
* Root directory: “/”
* Current directory: “.”
* Parent directory: “..”
* User’s home directory: “~“
* Globbing: “$*$”
#### Current working directory (cwd)
* Locality
	* `./a.out` will refer to different files in different contexts
* Shells track a **default list of active contexts**
	* The list is referred to as a ==search path== for programs you can run

## [[Hard Links]] & [[Soft Links]]
* More than one directory entry can refer to a given file

## [[Speeding up FS]]


## [[Fragment Allocation]]

## [[Block Allocation]]

## Cluster writes
* FS delays writing a block back to get more blocks
* **Accumulates blocks into 64K clusters, written all at once**
Allocation of clusters similar to fragments and blocks
* System maintains a cluster bitmap
	* One bit for each 64K if entire cluster is free

## [[Crash Recovery]]
## [[XFS]]
## [[Contiguous Allocation]]
* Want each file contiguous on disk
	* Sequential file I/O should be as fast as sequential disk I/O

