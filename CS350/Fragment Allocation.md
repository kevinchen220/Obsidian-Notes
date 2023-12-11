# Fragment Allocation
## When is a new fragment created?
**When system must allocate space when user writes beyond end of file**
* Allow last block to be a fragment to reduce internal [[Fragmentation#Internal Fragmentation|internal fragmentation]]
#### Problem
* Slow for small writes
#### Partial Solution
* Create a new `stat` struct field `st_blksize`
	* Tells applications file system block size