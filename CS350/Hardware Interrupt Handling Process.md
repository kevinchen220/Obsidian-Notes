# Hardware Interrupt Handling Process
1. Finds the [[Interrupt Descriptor Table]] through IDT Register
2. Reads the IDT descriptor entry for that particular interrupt vector
	* 60 for `syscall`
3. IST field specifies which stack to use
4. Looks up kernel stack location in the TSS
	* Provides information about a particular task
5. CPU pushes the interrupt stack frame onto this stack
6. Then the [[OS Kernel|kernel]] pushes the [[Trapframe]]
7. Then it sets up the CPU to known state to run C code