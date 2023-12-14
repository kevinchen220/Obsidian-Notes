---
dg-publish: true
---
# SJF Scheduling

> [!tldr] Schedule the job whose next CPU burst is the shortest

### Two schemes:
**Non-preemptive**
* Once the CPU is given to the process it cannot be pre-empted until it completes its CPU burst
**Preemptive**
* ==Shortest-Remaining-Time First== (SRTF)
* If a new process arrives with a CPU burst length less than remaining time of current process → pre-empt and run new one

> [!tip] SJF gives the **minimum average waiting time** for a given set of processes

## Limitations
##### SJF doesn’t always minimize the average turnaround time
* Only minimizes waiting time
**SJF can lead to unfairness or starvation of** jobs of longer burst
* They never run if shorter jobs keep coming in
#### Estimate CPU burst length based on past bursts
**Use exponentially weighted average**
* $t_n$ actual length of process’s $n^{th}$ CPU burst
* $\tau_{n+1}$ estimated length of process’s n+1 burst
* Choose parameter $\alpha$ where $0<\alpha<1$
* Let $\tau_{n+1}=\alpha t_n+(1-\alpha)\tau_n$
	* Large $\alpha$ will put more weight on the actual length of the last burst $t_n$
	* Small $\alpha$ will put more weight on the estimated length of last burst $\tau_n$
	* 
