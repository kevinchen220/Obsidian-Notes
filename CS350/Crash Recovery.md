---
dg-publish: true
---
# Crash Recovery
## Fixing Corruption
**Must run FS check `fsck` utility after a crash**
* File system summary info is usually inaccurate right after a crash
	* Scan the file system to check free block map, block/[[inode]] counts
* System may have corrupt inodes
	* Bad block numbers
	* [[Cross-allocation]]
	* Do sanity check
		* <u>Clear node with garbage</u>
* Fields in inodes may be wrong
* Count number of directory entries to verify link count
	* If not entries but count $\neq$ 0, move to **lost+found**
* [[Directories]] may be bad
	* `.` and `..` must be valid, and file names must be unique
	* All directories must be reachable

## Idea: Ordering of Updates
**OS must always update the file system components in a consistent order**
#### Solution
Make metadata updates asynchronous
* Doing one write at a time ensures consistent ordering
* Hurts performance
System cannot update buffers on the disk queue
* Blocks that are waiting to be written

## Performance vs. Consistency
#### Crash recoverability comes at a huge cost
* Makes some tasks 10-20x slower
### Solution: Battery packed RAM
* Expensive
* Battery might die
* OS bug causes crash
	* RAM might be garbage

## [[Soft Updates]]

## Soft updates `fsck`
Split `fsck` into foreground and background parts
* Foreground must be done before remounting FS
	* Make sure per-cylinder summary info makes sense
	* Recompute free block/inode counts from bitmaps
	* Will leave FS consistent, but might leak disk space
* Background does traditional `fsck` operations
	* Do after mounting to recuperate free space

## [[Journaling]]

## Journaling vs. Soft Updates
##### Both are much better than FFS alone
#### Limitations of soft updates
* Very specific to FFS data structures
* Metadata updates may proceed out of order
* Need slow background `fsck` to reclaim space
#### Limitations of journaling
* Disk write required for every metadata operation
* Possible contention for end of log on multi-processor