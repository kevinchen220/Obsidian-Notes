> [!tldr] Generated by devices to signal they need attention
>

> [!example] 
> * Input is ready
> * packet arrived from internet
### Interrupt Handler
**Function in the [[OS Kernel|kernel]] that services a device request**
Interrupt process:
1. Device signals the processor through a physical pin or bus message
2. Processor interrupts the execution of current running program
3. Begins executing interrupt handler in [[Kernel mode]]

> [!NOTE] Most interrupts can be disabled
> Non-maskable interrupts are for urgent system requests
> * Overheating
### Configuration
1. The OS initializes the [[Interrupt Descriptor Table|IDT]] with entry points for up to 256 interrupts
2. OS initializes IDT base address and length
3. OS executes `lidt` instruction to load the IDT Register
![[Pasted image 20231208164712.png]]
### [[Hardware Interrupt Handling Process]]