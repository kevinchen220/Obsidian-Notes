
> [!tldr] Algorithm to detect [[Concurrency#Critical Section|data races]] 

For each global memory location, keep a lockset
* Vector keeping tack of locks
	* (1, 1, 1, 1)
On each access of a global memory location
* Note any locks not currently held
	* Denoted by 0
**If lockset becomes empty (0, 0, 0, 0) → there is no mutex protecting this memory location**

> [!NOTE]
> We do not check specific locks for specific global variables
> We check if **any** locks are being held




