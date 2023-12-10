# Base + Bound Register
## Idea
* Two special privileged registers **base** and **bound**
* On each load or store:
	1. Calculate the physical address = virtual address + **base**
	2. Check 0 ≤ virtual address < **bound** else address ERROR

> [!question] How to move process in memory?
> Change **base** register

> [!question] What happens on context switch?
> OS must re-load **base** and **bound** register

## Advantages
* Inexpensive in terms of hard ware
	* Two registers
* Inexpensive in terms of cycles
	* Add and compare in parallel
## Disadvantages
* Growing a process is expensive
* No way to share code or data
* 