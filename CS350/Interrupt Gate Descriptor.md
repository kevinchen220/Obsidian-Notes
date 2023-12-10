# Interrupt Gate Descriptor
![[Pasted image 20231208164141.png]]
**Target Offset**: Address of the first instruction of the interrupt handler
**Target Selector**: Sets privilege level
**P**: Present, is it a valid entry
**Description Privilege Level**: Minimum privilege level that can trigger interrupt
* Prevents user programs from triggering device interrupt
**Type**: Identifies as 64-bit IDT entry
**IST**: Kernel stack to use