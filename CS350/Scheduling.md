---
tags:
  - unit
  - cs350
---
# Scheduling
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

**Scheduling decisions may take place when a process**
1. switches from running to waiting state
2. switches from running to ready state
3. switches from new/waiting to read
4. exits
Non-preemptive schedules use 1 and 4 only
See also [[Process states]]
## [[Scheduling Criteria]]

## Bursts of Computation and I/O
Jobs contain I/O and computation
* Bursts of computation
* Followed by waiting for I/O
**To maximize throughput**
* Must maximize CPU utilization
* Maximize I/O device utilization
How?
* Overlap I/O and device computation from multiple jobs
* 
## Approach 1: [[FCFS Scheduling]]
* Scheduling algorithm can reduce turnaround time
	* Schedule shorter tasks first
## Approach 2: [[SJF Scheduling]]
* Attempts to minimize turnaround time
## Approach 3: [[Round Robin Scheduling]]
* Addresses fairness and starvation
## Approach 4: [[Priority Scheduling]]
## Approach 5: [[Borrowed Virtual Time Scheduler]]

## Multiprocessor Scheduling Issues
**The scheduler also needs to decide on which CPU/core runs which process**
* Moving between CPUs/cores has costs
	* More RAM cache misses
	* More TLB misses
		* depending on architecture
#### Affinity scheduling
* Try to keep threads on same CPU/core
## [[Context Switch]] Costs
#### Direct cost
* Processor time costs in the kernel
	* Save and restore registers
		* For [[System Calls]]
	* Switch address space
#### Indirect Costs
* More cache misses in
	* RAM cache
	* [[TLB]]
	* System’s file buffer cache

## [[Time Quantum]]

## [[Thread Dependencies]]
