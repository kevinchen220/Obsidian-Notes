# Thrashing

> [!tldr] When an application constantly swapping pages in and out
> * Very slow


> [!NOTE] Cause
> * Process requires more memory than system has
> 	* Each time a page is brought in, a page that will need to used later is evicted
> * Memory access pattern does not exhibit [[temporal locality]]
> 	* [[80⧸20 Rule]] does not apply

## Approach 1: Working Set Model
According to [[80⧸20 Rule]], some portion of the address space will be heavily used and the remainder will not.
* Call the heavily used portion the **working set**
	* Changes across phases of using a program
* Set of pages in currently in primary memory is **resident set**

> [!question] Given locality of reference, how big a cache does the process need?
> Only run processes whose memory requirement can be satisfied

## Approach 2: Page Fault Frequency
**PFF = page faults / instructions executed**
* If PFF rises above high threshold → needs more memory
* If PFF sinks below low threshold → can take away memory
 ![[Pasted image 20231209182000.png]]
 





