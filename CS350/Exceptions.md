---
dg-publish: true
---
# Exceptions
> [!tldr] Conditions discovered by the processor while executing an instruction

> [!Example] 
> * Program error: Divide by 0
> * OS requests: [[Page fault]]
> * Hardware error: internal processor error

[[Processes]] handle exceptions similar to [[Interrupts]]
1. processor stops at the instruction that triggered the exception
2. control is transferred to a fixed location where the exception handler is located
3. execute in [[Kernel mode]]


> [!info] [[System Calls]] are a class of exceptions
