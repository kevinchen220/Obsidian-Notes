---
tags:
  - unit
  - cs350
dg-publish: true
---
# Concurrency
> [!tldr] Multiple programs running, or appearing to run at the same time

## Parallelism
* ==run at the same time== because of multiple core processors or multiple processors

> [!example]
> A company hires 90 workers to make 90 widgets and have them work in parallel
> * It takes 1 worker 10 months to make 1 widget
> * [[Speed#Low latency|Latency]] for first widget can be >> 1/10 month
> 	* Throughput may be < 10 widgets per month
> 	* If no perfectly parallelized
> 
> 100 workers making 10,000 widgets may achieve > 10 widgets / month
> * if for part of the process they have to wait for ==some subtask to complete==
> 


## [[Protection#Pre-emption|Preemptive]] [[Multitasking]]
* ==Appearing to run at the same time==
	* Rapidly switching between programs

## [[Critical Section]]
- Data races occur without [[Synchronization]]
	- Accessing same global variable
- Race condition
	- When program result depends on order of execution

> [!done] Solution
> Atomic instructions
> * Use processor features to make it look like you made the update instantaneously
> 
> [[Mutex|Locks]]
> * Prevent concurrent execution of certain instruction by different threads


> [!NOTE] Sometimes we allow for race conditions
> Provides greater efficiency
> * number of hits on a website
> * more concerned with speed than accuracy

### Detecting data races
* Static methods
	* detected by compiler
* Instrumentation
	* modify the program to check memory accesses
* [[Lockset Algorithm]]
	* effective

## [[Sequential Consistency]]
* Usually assume sequential consistency
* If we obey certain rules, it should be indistinguishable from sequential consistency
## [[x86 Consistency]]
## [[x86 Atomicity]]
## [[Mutex]]
* Busy waiting is inefficient
	* Thread consumes processor time even though doing nothing
	* Slows down other threads and processes
## [[Condition Variables]]
* Inform scheduler which threads can run
## [[Monitors]]
## [[Semaphores]]
