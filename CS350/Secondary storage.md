> [!tldr] State info that does not disappear
> **This is where all important state resides**
> * Persistent storage
### Overview
**Secondary storage reads and write in units of sectors** (larger than bytes)
> [!question] How do we modify a single byte?
> 1. Read entire sector
> 2. Modify byte
> 3. Write back entire sector

Sector is unit of atomicity
* Sector write is always done completely
### Magnetic Disk vs. Flash Memory
![[Pasted image 20231209193609.png]]
**Cost vs. Performance**
* Disk is cheaper, flash is faster
* Flash write performance degrades over time


> [!tip] Trends
> Hard disk **bandwidth** and **cost per bit** improving exponentially
> Seek time and rotational delay improving very slowly
> * ==Requires moving physical objects==
> * Bottleneck


