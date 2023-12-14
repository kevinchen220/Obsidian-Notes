---
tags:
  - unit
  - cs350
dg-publish: true
---
# I⧸O and Devices
![[Pasted image 20231210224228.png]]
#### A CPU accesses physical memory over a **[[Bus]]**
* Devices access memory over I/O bus with [[Direct Memory Access|DMA]]
* Devices can appear to be a region of memory
	* [[Memory-mapped IO]]
* A **crossbar** can connect any input to any output
#### A **bridge** connects two different buses
The **I⧸O Advanced Programmable Interrupt Controller** handles interrupts from devices

## What is [[memory]]?
## Communicating with a device
#### Memory-mapped device registers
* Some ranges of physical addresses correspond to device registers
* Load and store instructions get status or sends instructions to a device
#### Device memory
* Device may have memory and the OS can write directly to the device through I/O [[Bus]] rather than RAM
#### [[Direct Memory Access]] (DMA)
* Place instructions to device in main memory

> [!example]
> Parallel Port
> * Every bit corresponds to a pin
> 
> There are three primary types of device registers
> * **Status**
> 	* Tells something about device current state
> 	* Read
> * **Command**
> 	* Issue a command to the device
> 	* Write
> * **Data**
> 	* Used to transfer data to and from device

#### Using Physical Addresses
```c
volatile int32_t *device_control = (int32_t *) 0xc00c0100;
*device_control = 0x80; /* give command */
int32_t status = *device_control; /* get back status */
```
OS must map device addresses to virtual addresses and ensure they are non-cacheable
* `volatile` keyword tells compiler to not optimize
	* Read and write directly to RAM
* Assign physical address at boot time to avoid conflicts

## [[Device Drivers]]
## Anatomy of a [[Disk]]
## [[Flash memory]]
