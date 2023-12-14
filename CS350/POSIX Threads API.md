---
dg-publish: true
---
# POSIX Threads API
## pthread_create
```c
int pthread_create(
	pthread_t *thr, 
	pthread_attr_t *attr, 
	void *(*fn)(void *), 
	void *arg
);
```
* ### Create a new thread identified by `thr` which will execute `fn` with arguments `arg`.
* Can provide additional attributes through `attr`
	* stack size
	* `NULL` for default values
## pthread_exit
```c
void pthread_exit(void *return_value);
```
* ### Destroy current thread and return a pointer to its return value
## pthread_join
```c
int pthread_join(phtread_t thread, void **return_value);
```
* ### Wait for `thread` to exit and receive the return value
## pthread_yield
```c
void pthread_yield();
```
* ### Tell the OS scheduler to run another thread or process if available
* Wait until yield or preempted

## Also has lots of support for [[Synchronization]]

## [[Kernel Thread]] vs. [[User Thread]]
### Functions like `pthread_create` can be implemented as a function in either:
* **function call in user space** → inexpensive
* **[[System Calls|system call]] in kernel space** → expensive
#### Approach #1: Add `pthread_create` as a kernel thread (1:1)
![[Pasted image 20231207155201.png]]
* Uses less resources compared to creating a new process
	* Still expensive
	* System calls are expensive
**Limitations**
* Every thread operation goes through the kernel
	* 1:1 correspondence between user and kernel threads
	* ==thread operations are 10x-30x slower==
* Kernel threads must please all sorts of application needs
* Heavy-weight memory management

#### Approach #2: Add `pthread_create` as user thread (n:1)
![[Pasted image 20231207162927.png]]
* Many threads but only one kernel thread per process
* `pthread_create`, etc. are library functions
**Implementation**
* Allocate new stack for each `pthread_create`
* Keep queue of runnable threads
* ==Blocking== describes moving from a running state to waiting state
* Replace blocking system calls with non-blocking ones
* [[Protection#Pre-emption|Pre-emption]]
	* Switch to another thread on timer
**Limitations**
* ==Cannot take advantage of multiple cores or processors==
* Blocking system call blocks all threads
	* Cannot switch since that requires kernel
	* Uncached disk read
	* [[page fault]]
* Possible [[Deadlock]] if one thread blocks on another

#### Approach #3: User threads on kernel threads (n:m)
![[Pasted image 20231207163627.png]]
* Multiple kernel threads per process
* `pthread_create`, etc. are library functions
**Limitations**
* Many of the same problems as n:1 threads
* Kernel does not know importance of each thread
	* Might [[Protection#Pre-emption|preempt]] one holding an important lock