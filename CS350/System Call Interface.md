# System Call Interface
![[Pasted image 20231208114739.png]]
[[OS Kernel |Kernel]] supplies well-defined system call interface
* Applications set up syscall arguments and [[Trapframe|trap]] to kernel
* Kernel performs operation and returns result
Higher-level functions that programmers use are built on this interface
* `printf`, `scanf`, `gets`, etc.

> [!example] 
> [[POSIX Interface]]
> * Used by Linux and Unix
> 	* `open`, `close`, `read`, `write`, …

* Example with C standard library
![[Pasted image 20231206210651.png]]