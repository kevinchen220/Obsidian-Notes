---
dg-publish: true
---
# Round Robin Scheduling

> [!tldr] Addresses fairness and starvation
> Pre-empt job after some time slice or scheduling [[time quantum]]
> * When pre-empted, move to back of FIFO queue

### Advantages
* Fair allocation
* Low average waiting time **when job lengths vary**
	* Short jobs complete quickly
### Disadvantages
**For same sized jobs, round robin perform worse than [[FCFS Scheduling]]**



