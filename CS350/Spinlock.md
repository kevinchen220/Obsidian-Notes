> [!tldr] Repeatedly test the lock’s availability until lock is obtained
> Efficient for short waiting times

> [!example] 
> ```c
> mutex_lock(bool *mutex) {
> 	while (xchg(mutex, true) == true) {}; //test and set
> }
> ```
> 
> ```c
> mutex_unlock(bool *mutex) {
> 	*mutex = false;
> }
> ```
> Thread busy-waits in a loop until [[Mutex|mutex]] is acquired


> [!NOTE] [[Interrupts]] are disabled on the thread that holds a spinlock
> Thread will only execute a few instructions before releasing spinlock

### Implementation in CasterOS
```c
void Spinlock_Lock(Spinlock *lock)
{
	/* Disable Interrupts */
	Critical_Enter();
	while (atomic_swap_uint64(&lock->lock, 1) == 1)
	/* Spin! */;
	lock->cpu = CPU();
}
void Spinlock_Unlock(Spinlock *lock)
{
	ASSERT(lock->cpu == CPU());
	atomic_set_uint64(&lock->lock, 0);
	/* Re-enable Interrupts (if not spinlocks held) */
	Critical_Exit();
}
```


See also [[Hardware Specific Synchronization Instructions]]

