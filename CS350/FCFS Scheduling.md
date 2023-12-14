---
dg-publish: true
---
# FCFS Scheduling

> [!tldr] Run [[processes]] in order that they arrive
> 
## FCFS Convoy Effect
###### A long running job prevents many shorter jobs that are after it from running
* Without preemption, CPU-bound jobs will hold the CPU until they exit or require I/O
	* I/O is rare for CPU-bound threads
	* ==CPU is held==
* **Poor I/O device utilization**
	* Just waiting for the CPU
* 