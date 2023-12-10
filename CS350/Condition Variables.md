# Condition Variables
> [!tldr] Allow threads to wait for arbitrary conditions to become true
> Each CV corresponds to a particular condition that is of interest to an application


> [!example]
> - `cond_t nonempty` → `count > 0` (there are items in the buffer)
> - `cond_t nonfull` → `count < BUFFER_SIZE` (there is free space in the buffer)

When **condition is not true**, thread can `cond_wait` until condition becomes true
* Unlock the mutex, so not busy waiting
When another thread detects that **condition is true**, use `cond_signal` or `cond_broadcast` to notify blocked threads

> [!bug] Always recheck conditions on wake up
> ```c
> while (count == 0)
> 	cond_wait(&nonempty, &mutex)
> ```
> Do not use `if`
> * Condition may change

> [!question] Why must `cond_wait` both release mutex and sleep?
> Will [[Deadlock]] if sleep with locked mutex

> [!question] Why not separate mutexes and CV?
> Can end up stuck waiting when bad interleaving
> * Another thread acquires the same lock and signals


## [[PThread CV API]]
* Use [[Mutex]] to implement
	* Each `cond_wait` takes a mutex
		* To lock and check condition when awake
