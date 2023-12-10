> [!tldr] C11 built-in support for atomics

### `_Atomic(...)` wrapper
* Can wrap most basic types and they become atomic
* Operations become [[Sequential Consistency|sequentially consistent]]
### `atomic_flag`
* Atomic boolean value without support for loads or stores
* Can do `atomic_flag_test_and_set` and `atomic_flag_clear`
* Must be lock-free
	* Cannot be [[Protection#pre-emption|pre-emption]] in the middle of instruction

### Memory Ordering
1. **memory_order_relaxed**: no specific memory ordering required
2. **memory_order_consume**: slightly relaxed version of acquire
3. **memory_order_acquire**: reads and writes that happen after a lock cannot be moved before it
4. **memory_order_release**: All writes must be completed before release the lock, cannot be moved after
5. **memory_oreder_acq_rel**: Combination of 4 and 5
6. **memory_order_seq_cst**: Full [[Sequential Consistency]]
