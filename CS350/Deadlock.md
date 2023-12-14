---
dg-publish: true
---
# Deadlock
> [!tldr] Both threads stuck forever

> [!example] 
> ```c
> mutex_t m1, m2;
> 
> void f1(void *ignored) {
>   lock(m1);
>   lock(m2);
>   /* critical section */
>   unlock(m2);
>   unlock (m1);
> }
> 
> void f2 (void *ignored) {
>   lock(m2);
>   lock(m1);
>   /* critical section */
>   unlock(m1);
>   unlock(m2);
> }
> ```
> Dangerous to acquire locks in different orders
> 

## Conditions
1. Limited access (mutual exclusion)
2. No [[Protection#Pre-emption|pre-emption]] of resources
3. Multiple independent requests
4. **Circularity in graph of requests**

## Solution
### Prevention (eliminate one condition)
1. Limited access
	* But more resources
2. No pre-emption
	* Physical memory: virtualize with VM, can give same page to another process
3. Multiple independent requests
	* Wait on all requests
4. **Circularity in graph of requests**
	* Single lock for entire system
		* Inefficient
	* **Partial ordering of resources**
		* Always acquire mutexes in a specific order
			* `m1` before `m2`