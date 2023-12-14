---
tags:
  - unit
  - cs350
dg-publish: true
---
# Synchronization
## Motivation
[[Amdahl’s Law]] guides the **efficiency gains when using multiple cores**

## Locking Basics
* Only one thread can hold a [[Mutex|lock]] at a time
* **Never touch global data unless you hold the right lock**

## [[Fine-grained locking]] vs. [[Coarse-grained locking]]

## [[Hardware Specific Synchronization Instructions]]

## [[Cache Coherence]]
## [[MCS Lock]]
## [[Deadlock]]
## [[Wait Channel]]

## Hand-over-Hand Locking
* Fine-grained locking
* Useful for concurrent access to a single data structure
	* Hold at most two locks
		* The previous and the next
	* Must have order
		* or else [[Deadlock]]

> [!NOTE] [[Mutex]], [[Condition Variables]], [[Semaphores]] use [[Wait Channel]] and [[Spinlock]]
> Lock order:
> 1. Acquire spinlock **(exclusive access to struct’s fields)**
> 2. Acquire waitchannel lock **(exclusive access to waitchannel)**
> 3. Release spinlock **(we have access to what we want, WC)**
> 
> Spinlock that the wait channel uses is hidden in these calls

> [!example] 
> [[Semaphores#Implmentation]]

