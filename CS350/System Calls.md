---
dg-publish: true
---
# System Calls
#unit

> [!tldr] API that programmers use to interact with OS

### Special instructions that transfer control to the [[OS Kernel |kernel]]
* similar to a function call

> [!todo] ## Goal:
> * Execute functions that the app cannot do in unprivileged mode

## [[System Call Interface]]
## [[Kernel mode]] vs. [[User mode]]

## [[Interrupts]] & [[Exceptions]]
## System Call Order
> [!NOTE] System calls are performed by using the **T_SYS** exception vector
> 1. App loads the system call arguments into appropriate registers
> 2. Load system call number in to `%rdi`
> 3. Execute `int 60` instruction
> 	* `int` for interrupt, 60 corresponds to **T_SYS**
> 4. Processor looks up the interrupt vector in a table
> 5. Jumps to that address
> 6. When done, return to userspace and user mode using `iret`

![[Pasted image 20231208162702.png]]
## [[Interrupt Descriptor Table]]
## [[Application Binary Interface]]

## [[Function in x86]]