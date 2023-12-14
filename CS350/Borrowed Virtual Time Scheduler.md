---
dg-publish: true
---
# Borrowed Virtual Time Scheduler
### Idea
Equalize virtual CPU time consumed by different processes
* Run process with the lowest effective virtual time
* Effective virtual time = A_i - (warp_i ? W_i : 0)
	* A_i = actual virtual time consumed by process i
	* Warp factor allows borrowing against future CPU time

## Process weights
##### Each process i’s share of actual processor time is determined by its weight $w_i$
* Process i should get $w_i/\sum_jw_j$ fraction of the actual processor time
* When i consumes t processor time, track it as $A_i += t/w_i$
#### Problem
Lots of context switches
* Not good for performance
#### Idea
Add in context switch allowance, C,
* So each process runs for a bit of time, $C/w_i$ before preemption
* Only switch from i to j if $E_j\leq E_i-C/w_i$

## Sleep / wakeup
#### Must lower priority after wakeup
* Otherwise process with very low $A_i$ will starve the other processes
#### Have a lower bound on $A_i$ with a minimum time, Scheduler Virtual Time
* SVT is minimum virtual time
* When waking i from **voluntary** sleep $A_i = max(A_i, SVT)$
	* Don’t set for involuntary

## Real-time [[threads]]
#### Goal: Support soft real-time threads
* Threads that need to run within a certain time or performance will degrade
$E_i=A_i-(warp_i ? W_i : 0)$
* $W_i$ is **warp factor**
	* gives a thread precedence
	* It will get the CPU whenever it is runnable
* Long term CPU share won’t exceed $w_i/\sum_j w_j$
**$W_i$ only matters when $warp_i$ is true**
* Need two other parameters $L_i$ and $U_i$
* Can get $warp_i$ set with a [[system calls|system call]] or signal handler
	* Gets cleared if i keeps using CPU for $L_i$ time
	* $L_i$ limit gets reset every $U_i$ time