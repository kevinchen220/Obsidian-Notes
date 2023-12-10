> [!todo] Implement a [[Mutex|mutex]] atomically
> * No other thread can change its value between **testing** and **setting** the mutex

### Test-and-Set
```C
while (*mutex == true) {}; //  Test if mutex is held
*mutex = true; // set it to true
```
Testing to setting the [[Mutex|mutex]] should be done in one [[x86 Atomicity|atomic]] step
* We can use [[x86 Atomicity#`xchg`|xchg]] 
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
> `xchg(mutex, true)` returns the old value of `mutex`
> * If returns `true`, then mutex was previously held
> * If returns `false`, then mutex was not held and we are now holding it
> This is known as a [[Spinlock]]

> [!warning] A lot of variation for multithreaded code on different processors
> x64 has Complex Instruction Set with **total store order consistency**
> * A thread can read its own write and becomes visible to all other threads
> ARM has Reduces Instruction Set with **relaxed consistency**
> * Reads and writes can occur out of order, possible different order in different threads

### C11 has built-in support for atomics
* [[C11 Atomics]]
