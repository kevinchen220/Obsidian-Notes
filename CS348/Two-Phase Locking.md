---
dg-publish: true
---
# Two-Phase Locking
### DBMS Scheduler
1. Receives requests to execute operations from the query processor
2. For each operation it chooses one of the following actions
	1. **Execute** (send to a lower module)
	2. **Delay** (insert in some queue)
	3. **Reject** (abort transaction)
	4. **Ignore** (no effect)


> [!info] Types of Schedulers
> 1. **Conservative schedulers:** Favour delaying operations
> 2. **Aggressive schedulers:** Favour rejecting operations

## 2PL

> [!tldr] Conservative schedulers are lock based

#### Lock
* **Shared lock:** Required to read an object
* **Exclusive lock:** Required to write an object
	* Disallows any other lock at all to be hold on $x$ by any other transaction

> [!warning] Insufficient for a scheduler just to acquire a lock, access the data item, and release it immediately


> [!tip] 2PL
> Scheduler allows no lock to be acquired by a transaction $T$ on some object after the first lock by $T$ on some other object is released by $T$

**Theorem:** Any execution order of operations admitted by a scheduler following the two phase locking protocol will be a prefix of an ultimate schedule that is a [[Schedules#Serializable Schedules|conflict serializable schedule]] 


> [!warning] 2PL can still allow operations to process that lead to 
> 1. Cascading aborts
> 2. Deadlocl

#### Strict Two-Phase Locking
Scheduler allows no lock for a transaction $T$ to be released until $T$ requests either a commit or abort operation
**Theorem:** Any execution order of operations admitted by a scheduler following the strict two phase locking protocol will be a prefix of an ultimate schedule that is a conflict serializable schedule and will also have the [[Concurrency Control|ACA property]] ensuring no cascading aborts


> [!info] Variations on Locking
> * Multi-granularity locking
> 	* Not all locked objects have the same size
> 	* Advantageous in presence of bulk versus tiny updates
> * Predicate locking
> 	* Locks based on selection predicate rather than on a value
> * Tree locking
> 	* Can be used to avoid congestion in roots of Btrees
> 	* Allows relaxation of 2PL due to tree structure of data
> * Lock upgrade protocols

### [[Deadlocks]]
### [[Inserts and Deletes]]
### [[Isolation Levels]]

