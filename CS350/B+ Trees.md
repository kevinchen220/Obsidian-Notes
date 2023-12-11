# B+ Trees
Similar to [[B Trees]] in the following ways
* Both are indexed data structures that store ordered (key, value) pairs
	* Keys must have an ordering defined on them
* Both store data in blocks for efficient disk access

> [!tip] In B+ trees all the key-value pairs are in the leaves
> More keys can fit in interior nodes
> * Shorter and wider
> 
![[Pasted image 20231210202430.png]]
> Leaves are also connected as a linked list
> * Sequential access is easy

**For B+ tree with $n$ items, all operations are $O(\log n)$**
* Retrieve closest (key, value) pair to target key k
* Insert a new (key, value) pair
* Delete (key, value) pair
Some operations on B+ tree are complex
* e.g. insert item into completely full B+ tree
[[Journaling]] enables complex operations to be atomic
