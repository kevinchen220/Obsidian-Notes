# Priority Scheduling

> [!tldr] Associate a numeric property with each process
> Smaller number means higher priority

Give the CPU to the process with highest priority
**[[SJF Scheduling]] is a priority scheduling where priority is the predicted next CPU burst time**
### Starvation
* Low priority processes may never execute
#### Solution?
Aging
* Increase a process’s priority as it waits

## [[Multilevel feedback queues]]
* Every runnable process is on one of 32 run queues
	* **Kernel runs process on highest-priority non-empty queue**
* Process priorities are dynamically computed
	* Processes move between queues to reflect priority changes
	* If a process gets higher priority than the current one → run it
## [[Process Priority]]