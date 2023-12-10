### Primitive OS
![[Pasted image 20231206195659.png]]
* A library OS is a library of standard services
	* standard interface above hardware-specific drivers
* <u>Assumptions</u>
	* system runs one program at a time
	* no bad users or programs
> [!warning]- Problems
> * Poor utilization of hardware
>		* A lot of idle time
>		* Waiting for I/O
>	* Poor utilization of human user
>		* Have to wait for each program to finish running
* Used by simple devices like doorbell and thermostats

### [[Multitasking]] OS
![[Pasted image 20231206202455.png]]
* Can have multiple processes at the same time
	* When one process is blocked we can run another
> [!warning]- Problems: What can a bad process do?
> * Infinite loop
>		* All processes stuck
>	* Overwrite another process's memory

>[!success] Solutions to the problems above:
>* [[Protection]]
>	* ==Pre-emption==
>		* Take processor away
>	* ==Memory protection==
>		* Protect processes' memory from one another


### Multi-user OS
![[Pasted image 20231206202502.png]]
* Provide protection to bad users and buggy apps
	* So that they don't affect other users and apps
* The system does not slow linearly based on the number of users
	* user demand for processor is bursty, not uniform
> [!warning]- Problems
> * Users can use too much resources → <mark style="background: #BBFABBA6;">Need policies</mark>
>	* Total memory usage greater than machine has → <mark style="background: #BBFABBA6;">Must virutalize</mark>
>	* Super-linear slowdown with increasing demand
>		* Thrashing