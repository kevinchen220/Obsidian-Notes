---
dg-publish: true
---
# Paging
> [!tldr] Divide both virtual and physical memory up into small fixed-size pieces

**For each process, map its virtual pages to physical pages**
* Each process has its own separate mapping
**Allow OS to gain control on certain memory operations**
* Read-only pages trap to OS on write
* Invalid pages trap to OS on read or write
* OS has ability to change mapping and resume application

## Trade-offs
* **Eliminates [[Fragmentation|external fragmentation]]**
	* Every allocation is the same size
* Average internal fragmentation of 0.5 pages per segment

## Implementation
* Pages are fixed size, e.g. 4KB
	* Least significant 12 bits of address are **page offset**
	* Most significant bites are the **page number**
* Each process has a **page table**
	* The page table converts virtual page numbers to physical page numbers
	* Also includes bits for protection, validity, etc.
* On memory access, translate VPN to PPN, then add offset

## Making Paging Fast
On each memory reference
1. Check [[TLB]], if entry present get physical address faster
2. If not, walk to page tables, and then insert the translation into the TLB


> [!example] 
> Different kinds of paging
> * **Demand paging**
> 	* Only load pages from the executable file, if they are needed
> * **Copy-on-write**
> 	* Share a reference rather than a copy
> 	* Make copy when write happen

## [[Working Set Model]]
- Take advantage of [[80⧸20 Rule]]

## Restarting after [[page fault]]
**Hardware provides the [[OS Kernel|kernel]] with information about the page fault**
* Faulting virtual address
* Address of instruction that caused fault
**Idempotent instructions** are easy to handle
* An instruction that can be repeated many times and produce the same result
	* load word, store word
	* ==Increment is not==
### What to fetch?
**At least need to bring in page that caused page fault**

> [!question] Pre-fetch surrounding pages?
> * Reading two disk blocks approximately as fast as reading one
> * Big win if the application exhibits [[spatial locality]]

> [!tip] Zero out unused pages in idle loop
> Need 0-filled pages for stack, heap, etc.
> * Zeroing on demand is slower


> [!tip] Two-level TLBs
> * Better than going to main memory
> * Second level is larger than first level
> 	* Still want to maximize hit rate in L1 TLB
## [[Superpages]]
## [[Eviction Policies]]

## Naïve Paging
* Uses 2 I/Os per page fault
	* Swap out and swap in

## Page buffering
Reduce number of I/Os on the critical path
**Keep a pool of free page frames**
* On fault, still select victim page to evict
* But store page fetched from swap space into already free page from the pool
* Can resume execution while writing out victim page

## Page allocation
Can be global or local
* Global allocation doesn’t consider page ownership
	* Works well if $P_1$ needs 20% of memory and $P_2$ needs 70%
	* ==Doesn’t protect you from memory hogs==
* Local allocation isolates processes
	* Separately determine how much memory each process needs
	* Then choose an algorithm to determine which pages to evict in each process

## [[Thrashing]]