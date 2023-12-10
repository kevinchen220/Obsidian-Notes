# Cache Coherence
## Coherence
* Accesses to a single memory location in different caches should be the same
## Consistency
* Apparent ordering between multiple locations

## [[Multicore Caches]]

## 3-State Coherence Protocol
### Modified
* One cache has a valid copy
	* **Dirty**, needs write back
* Out of date copies in other caches are **stale**
* Invalidate all other copies before entering this state
### Shared
* One or more cache have valid copy
### Invalid
* Doesn’t contain up to date data

> [!NOTE] Transitions take 100 cc on smaller machines and up to 2000 cc on larger ones

## Core and Bus Actions
Each core has three possible actions that affect the cache
### Read (load)
* No intent to modify
* Enter **shared** state
### Write (store)
* Intent to modify
	* Invalidate all other cache copies
* **Modified** state
### Evict
* Writeback to memory if modified
	* Only if in **modified** state

> [!warning] Performance problems
> * Every transition requires bus communications
> * Avoid state transitions where possible

### Implications for Multithreaded Design
1. **Avoid false sharing**
	* Avoid placing data used by different threads in the same cache line
2. **Align structures to cache lines**
	* Place related data you need to access together
3. **Pad data structures**
	* Add unused fields to ensure alignment
4. **Avoid contending on cache lines**
	* Reduce costly cache coherence traffic

## Real World Coherence Costs
> [!Example]
> Assume access time for an Intel Xeon processor caches and RAM:
> * 3 cycles for L1 caches
> * 11 cycles for L2
> * 44 cycles for last level caches (LLC)
> * 355 cycles for RAM
> 
> For different cores on the same processor
> * Load: 109 CC
> * Store: 115 CC
> * Atomic compare-and-swap: 120 CC

### Non-uniform memory access (NUMA)
Multiple processors, each processor has local memory
* Able to access local memory fast
For cores accessing data on different processors:
* NUMA load: 289 CC
* NUMA store: 320 CC
* NUMA atomic compare-and-swap: 324 CC
