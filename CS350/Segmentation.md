> [!tldr] Let process have many base and bound registers
> * [[Address Space]] built from many segments
> * Can share/protect memory at segment granularity
> * Segments provide different protection
> 	* Read-only, executable, etc
> See also [[Base + Bound Register]]
### Mechanics
![[Pasted image 20231209135523.png]]
* Each process has its own segment table
* Each virtual address is divided into a **segment number and offset**


> [!question] How do you find physical address?
> 1. Is it a valid segment number?
> 2. Check offset < segment length (Bound)
> 3. Check operation is allowed
> 4. Physical address = base + offset

### Advantages
* Allows multiple segments per process
* Allows sharing
* Don’t need entire process in memory
### Disadvantages
* Requires address translation hardware
* Segments not completely transparent to program
* **n byte segment need n contiguous bytes of physical memory**
* [[Fragmentation]]
