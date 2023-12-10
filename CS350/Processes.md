#unit
#### Processes are one of the abstractions commonly part of an OS. 
![[Pasted image 20231206210814.png]]
### What are Processes?
* <mark style="background: #BBFABBA6;">Instance of a running program</mark>
	* Not always a one-to-one match
	* Multiple MS Word run on one process
	* Browsers have separate process for each website
		* If the process crashes we only lose one tab

### Why do modern OSes run multiple processes at the same time?
* <mark style="background: #BBFABBA6;">Simplicity of programming</mark>
	* Programmers do not need to care about other running processes
* <mark style="background: #BBFABBA6;">Robustness</mark>
	* Program with bugs should not crash other processes or OS
* [[Speed#Higher Throughput|Higher throughput]]
	* Better processor utilization
* [[Speed |Low latency]]
	* time between action and getting a response

### Process’s view of the Computer
* From the process’s POV, it is the only thing running
> [!important] Each process has its own
> * [[Address Space]]
> * open files
> * virtual CPU
> 	* through [[Concurrency#Protection Pre-emption Preemptive Multitasking| Pre-emptive multitasking]]

> [!question] What if we still want interaction between processes?
> * Use files
> * More complicated:
> 	* Shell/command

### Two views of processes
* [[User view]]
* [[Kernel view]]

### [[Implementation of Processes]]

### [[Scheduling]]
- which process gets to run
### [[Context Switch]]
- Changing the running process
