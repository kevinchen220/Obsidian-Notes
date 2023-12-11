# Time Quantum

> [!question] How to pick quantum?
> * Want it much larger than context switching cost
> * Want the quantum to be larger than the majority of bursts
>
> Typically 10-100ms

## Turnaround time vs quantum
* Average turnaround time has local minima when the time quantum is the size of one of the process times
* Global minimum is when the quantum size is greater than or equal to most of the process times
![[Pasted image 20231210214056.png]]