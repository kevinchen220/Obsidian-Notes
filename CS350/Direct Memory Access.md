---
dg-publish: true
---
# Direct Memory Access

> [!tldr] Place instructions to device in main memory

## DMA Buffers
#### Idea: Use processor to give commands to transfer data
Let device manager transfer

> [!question] Why?
> Interacting with device is slow
> Frees up processor for other tasks

Include a list of buffer locations in main memory to transfer
* Start address and length

### Example
##### Network Interface Card
![[Pasted image 20231211081804.png]]
##### IDE disk read
![[Pasted image 20231211081849.png]]