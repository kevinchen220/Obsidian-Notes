# Eviction Policies
## FIFO Eviction
* **Evict oldest fetched page**
### [[Belady’s Anomaly]]

## Optimal Page Replacement
* **Replace page that will not be used for longest period of time in the future**
	* Of course we don’t know the future

## LRU Page Replacement
* **Replace least recently used**
	* Past behaviour often predicts future behaviour

> [!warning] LRU can give the worst possible result

### Implementations
1. Stamp entries with timer value
	* Scan pages to find oldest value
	* **Expensive**
2. Keep doubly linked list of pages
	* **Also expensive**
==Use Approximate LRU==

## Clock Algorithm
![[Pasted image 20231209173541.png]]
Use accessed bit to keep track of entries
* Write 1 to **A** in the PTE on first access
**Do FIFO but skip accessed pages**
1. If page’s **A** bit = 1
2. then set to 0 and skip
3. else evict
![[Pasted image 20231209174358.png]]
**Add a second clock hand**
* Leading hand clears **A** bit
* Trailing hand evicts pages with **A=0**
Can also use dirty bit
* Evict clean pages before dirty ones

## Random eviction