---
dg-publish: true
---
# Memory Management Unit
![[Pasted image 20231209130929.png]]
* Maps virtual address to physical address
* Enforces protection
	* Prevents one app from messing with another app’s memory
* Allows programs to see more memory than exists
	* Maps some memory accesses to [[Secondary storage]]

## Software Managed
* Simpler hardware which asks software to reload pages
* Requires fast exception handling and optimized software
* Enables more flexibility in the [[TLB]]

> [!example] MIPS MMU
> * Hardware has 64-entry [[TLB]]
> * TLB Entries: 64-bit
> 	* PID: Process ID
> 		* Allows multiple processes to use TLB
> 	* N: No Cache
> 	* D: Writeable
> 	* V: Valid
> 	* G: Global
> 		* Pages shared across all address spaces
> 
> ![[Pasted image 20231209151314.png]]
### MIPS TLB Instructions
* `tlbwr`: TLB write a random slot
* `tblwi`: TLB write a specific slot
* `tlbr`: TLB read a specific slot
* `tlbp`: Look for the entry that matches `c0_entryhi`
Need to load information into registers
* `c0_entryhi`: high bits of TLB entry
* `c0_entrylo`: low bits of TLB entry
* `c0_index`: TLB Index

### Exceptions
**UTLB Miss**
* user segment page number not found in TLB
**TLB Miss**
* kernel segment page number not found in TLB
**TLB Mod**
* Generated when writing to read-only page

> [!NOTE] UTLB handler is separate from general [[Exceptions|exception]] handler
> * UTLBs are very frequent and require a hand optimized path

### Hardware lookup algorithm
1. If the most significant bit is 1 and in user mode → address error exception
	* virtual address ≥ 0x8000 0000 (kernel memory)
2. If no VPN match → TLB/UTLB miss exception
3. If PID mismatch and global bit not set → TLB/UTLB miss
4. If valid bit not set → TLB/UTLB miss
5. Write to read-only page → TLB mod exception
6. If N b it is set → directly access device memory

## Hardware Managed
* Hardware reloads [[TLB]] with pages from a page table
* Typically hardware page tables are Radix Trees
* Requires complex hardware

> [!example] x86
> [[TLB]] managed by Hardware and Microcode
> * Two levels of TLBs each acting as a cache
> * **TLB automatically reloaded from page table by processor**
> OS builds Radix tree describing memory layout
> Contains much of the same information as MIPS
> * Global page
> 	* all processes can access it
> * Accessed
> 	* whether the page has been accessed recently
> * Cache disabled
> 	* do not store in cache
> * Write-through
> 	* enable write-through
> * User/Supervisor
> 	* privilege needed to access page
> * Read/Write
> 	* is the page writeable
> * Present
> 	* in RAM rather than is swap space on the SSD
> Directories ignore the global page bit
> Specifies page size instead of Page Table Attribute
> 

### x86 [[Paging]]
Normally 4KB pages
* Page directory
	* 1024 PDEs (page directory entries)
	* Each contains physical address of a page table
* Page table
	* 1024 PTEs (page table entries)
	* Each contains physical address of virtual 4K pages
![[Pasted image 20231209160411.png]]
