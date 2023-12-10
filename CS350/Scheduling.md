> [!tldr] Decide which process to run

> [!quesiton] Which process should the kernel run?
> * if 0 are runnable → **run idle loop** or halt CPU
> * if 1 is runnable → run it
> * if >1 are runnable → **must make scheduling decision** about which process to run
> 	* We could use a queue for runnable processes

> [!question] When to [[Protection#Pre-emption|pre-empt]]?
> Can preempt a process when control is passed to the [[OS Kernel]]
> * [[System Calls]], [[page fault]], illegal instruction
> * My put current process to sleep and make others runnable
> 
> **Device [[Interrupts|interrupt]]**
> * Disk request complete, packet arrived on network
> 	* Previously waiting task becomes runnable
> * Schedule if higher priority

Changing the running process is called a [[Context Switch]]