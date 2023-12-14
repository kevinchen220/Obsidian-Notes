---
dg-publish: true
---
# FAT

> [!tldr] Used linked files, but links reside in fixed-size **file allocation table**
> ![[Pasted image 20231210143908.png]]

Can cached entire FAT so can be cheap compared to disk access

> [!Example] 
> Entry size = 16 bits
> * What’s the maximum size of the FAT?
> 	* $2^16$ = 65536 entries
> * Given a 512 byte block, what is the maximum size of FS?
> 	* $2^16 \times 2^9=2^{25}$=32MiB
> 
> Reliability
> * How to protect against errors?
> 	* Create duplicate copies of FAT on disk
> 
> Bootstrapping
> * Where is root directory
> 	* Fixed location on disk



