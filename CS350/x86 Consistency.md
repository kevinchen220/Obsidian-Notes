
> [!NOTE] x86 supports multiple consistency/caching models
> Memory Type Range Registers (MTRR) 
> * Specify consistency for a few ranges of physical memory
> 
> Page Attribute Table (PAT)
> * Allows control for each 4k page

#### Caching choices:
* **WB**: Write-back caching
	* Write to cache and mark dirty bit
	* Write back to main memory when item is going to be removed from cache
	* ==More difficult to implement==
* **WT**: Write-through caching
	* All writes immediately written to main memory
	* ==Writes take longer==
* **UC**: Uncacheable
	* Values should not be stores in cache
* **WC**: Write-combining
	* Writes are temporarily stored in a buffer and occur in a burst
	* [[#Weak-consistency]] and no caching
	* Used for frame buffers
		* Sending a lot of data to GPU

#### Weak-consistency
* No guarantee that reads and writes will have [[Sequential Consistency]]
* ==Some instructions can be reordered==
	* String instructions
		* Can store in different order as long as we access it the same order
* ==Non-temporal instructions==
	* `movntq` for `movq`, not the `nt`
		* Non-temporal hint
		* data will not be used for a while so no need to cache
	* Bypass cache and can be reordered with respect to other writes
* 