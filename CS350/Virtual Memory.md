#unit 

> [!tldr] Manage memory to allow multiple processes to share it

> [!Warning] Issues in sharing physical memory
> Protection
> * Bug in one process can corrupt memory in another
> * Prevent *A* from trashing or observing *B*‘s memory
> Transparency
> * Process shouldn’t require particular physical memory bits
> Resource Exhaustion
> * Programmes typically assume machines has enough memory
> * Sum of sizes of all processes often greater than physical memory

### Goal
**Give each program its own virtual [[Address Space]]**
* At run-time, the [[Memory Management Unit]] relocates each load and store address to the actual physical address
### Advantages
* Relocate program while running
	* Store partially in memory and partially in SSD
* Most of process’s memory may be idle ([[80⧸20 Rule]])
	* Write idle parts to disk until needed

### Definitions
#### Virtual address
* Where programs load and store to
#### Physical address
* Where actual memory is
### Idea 1: [[Load-time Linking]]
### Idea 2: [[Base + Bound Register]]
### Idea 3: [[Segmentation]]
### Idea 4: [[Paging]]

### Where does the OS live?
**Kernel addresses are in the same address space as the user process**
* Use protection bits to prohibit user code from reading and writing kernel adresses
Typically all kernel text and most data are at **same virtual address in every address space**, upper half of memory

### Breakpoint
**Top of heap**
* Memory between breakpoint and stack is invalid
![[Pasted image 20231209182234.png]]

### VM [[System Calls]]
```c
char *brk(const char *addr);
```
* Set and return new value of breakpoint
```c
char *sbrk(int incr);
```
* Increment breakpoint and return old value
#### [[Memory mapped files]]

### Exposing page faults
`sigaction` is used to specify what action to take for **SIGSEGV** (invalid memory access)
```c
struct sigaction { /* the Linux struct for signal actions */
	union { /* system will have one of these signal handlers */
		void (*sa_handler)(int);
		void (*sa_sigaction)(int, siginfo_t *, void *);
	};
	sigset_t sa_mask; /* signal mask to apply */
	int sa_flags; /* options, e.g. for dealing with children */
};
int sigaction (int sig, const struct sigaction *act, struct sigaction *oact)
```

### VM Tricks
* Combination of `mprotect` and `sigaction`
	* Achieve kernel-like actions
* Technique used in object-oriented databases
	* Bring in objects on demand
	* Keep track of objects that are dirty
	* Manage memory as a cache for large DB objects

### [[Pmap Layer]]

