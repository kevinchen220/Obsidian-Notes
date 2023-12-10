#unit
![[Pasted image 20231207145558.png]]

> [!tldr] Thread is a sequence of instructions

> [!question] What are threads?
> Schedulable execution context
> * something that could execute on a core but also includes its the global context
> 
> Used to run multiple tasks that a process is responsible for **at the same time**
### [[Implementation of Threads]]

> [!question] Why use threads?
> * **Lighter weight** than processes
> * Allows processes to use multiple processors or cores in [[Concurrency#Parallelism|parallel]]
> * Allows a single program to overlap its I/O and computation

> [!tip] Typically at least one [[Kernel Thread]] for every process

### Threads vs. Procedures
* Threads may resume out of order
* Procedures are LIFO
* Thread can make many procedure calls
* More than one thread can run at a time
	* Only one procedure runs at a time

### Switching Threads
#### General (from [[OS Kernel|kernel]])
![[Pasted image 20231207185732.png]]
#### Hardware [[Interrupts|Interrupt]] (timer)
![[Pasted image 20231207185802.png]]
#### `Sched_Scheduler()`
* Determine which thread to run next
#### Sched_Switch()
- Switch the running thread
### [[Trapframe]] vs [[Switchframe]]



