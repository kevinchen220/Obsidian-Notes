---
dg-publish: true
---
# Directories

> [!tldr] A way to organize files


> [!tip] Directories are a type of file except a field in the [[inode]] identifies them as directories

### Approach 1: Single directory for entire system
* Put directory at known location on disk
* Directory contains `<name, inumber>` pairs
* Can’t have the same name for files
### Approach 2: Single directory for each user
* Still slow
### Approach 3: Hierarchical name spaces
* Allow directory to map names to files or directories
* File system forms a tree
#### [[Hierarchical UNIX]]

### Structure
**Directory contents are broken into 512 byte chunks**
* Each chunk has `direct` structure
	* 32 bit i-number
	* 16 bit size of directory entry
	* 8 fit file type
		* e.g. directory, file
	* 8 bit length of file name
* Coalesce when deleting
	* If first `direct` in chunk deleted, set i-number = 0
	* Don’t reuse entries, add to the end
* 