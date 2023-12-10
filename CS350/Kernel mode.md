
> [!tldr] Privileged mode used by the OS
### Access privileged processor features
* restricted processor features and registers
* Enable and disable [[Interrupts]], set up interrupt handlers
* Controls the [[System Call Interface]]
* Can modify [[TLB]]
* can interact directly with the peripherals

> [!todo] Allows [[OS Kernel|kernel]] to protect itself and isolate [[Processes]] from each other
> * Processes cannot read or write kernel memory
> * Processes cannot directly call kernel functions

> [!NOTE] Kernel mode can only be accessed through well defined entry points
> * [[Interrupts]]
> * [[Exceptions]]


> [!info] Interrupts, exceptions and [[System Calls]] use the same mechanism
> ![[Pasted image 20231208162343.png]]
> See also [[Trapframe]]


