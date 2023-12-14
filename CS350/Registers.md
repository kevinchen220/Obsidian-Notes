---
dg-publish: true
---
# Registers

> [!NOTE] We use x64 not MIPS

## Register names
* start with `%`
* many are named after what they do
	* e.g. `%rsp`
## Passing arguments
* pass the first 6 args in registers
* pass the rest on the stack
## Saving registers
### Caller-save
* **Not preserved across subroutine calls**
* Caller must restore value from stack
### Callee-save
* **Preserved across subroutine calls**
* subroutine restores it at the end

> [!goal] Minimize situations where we save registers that do not need to be saved
