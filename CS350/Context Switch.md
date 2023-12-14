---
dg-publish: true
---
# Context Switch
> [!tldr] Changing the running process
## A context switch is non-negligible cost
* Saving floating point
* Flushing TLB
* More cache misses
![[Pasted image 20231207144701.png]]

> [!question] What needs to be done?
> * Always save program counter and integer registers
> * Save floating point or other special registers
> * Save condition codes
> * Change [[Virtual Memory#Virtual address|virtual address]] translations


