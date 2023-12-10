# x86 Atomicity
## `lock` (prefix)
* Makes the memory instruction atomic
* Locks memory bus for duration of instruction
	* ==Expensive!==
* All lock instructions totally ordered
* Other memory instructions cannot be re-ordered with locked ones
## `xchg`
* **Always locked**
* Exchanges value stored in register with value stored in memory
	* `xchg src, addr`
* Returns the old value, `src`
## `cmpxchg`
* **Always locked**
* Compares two values and exchanges them if different
## `lfence` (load fence)
* Wait until all loads before the `lfence` are done before continuing
	* Load instructions cannot be moved from before the fence to after the fence
## `sfence` (store fence)
* Waits until all stores before the `sfence` are done before continuing
	* Store instruction cannot be moved from before the fence to after the fence
## `mfence` (memory fence)
* Waits for loads and stores
* Combination of `lfence` and `sfence`

