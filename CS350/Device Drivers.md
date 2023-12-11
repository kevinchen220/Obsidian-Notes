# Device Drivers

> [!tldr] Device driver provides several commands to the kernel

## Architecture

> [!question] How should the driver synchronize with device
> Need to know when the request is complete or if there was an error

#### Approach 1: Polling
* Sending a packet?
	* Loop asking card when buffer is free
* Waiting to receive?
	* Keep asking card if it has packet
* Disk I/O?
	* Keep looping until disk ready bit set
##### Disadvantages
- **Cannot use CPU for anything else while polling**

#### Approach 2: Interrupt driven devices
**Ask device to interrupt processor when event happens**
* Interrupt handler runs at high priority
* Handler asks device what happened
Bad under high network packet arrival rate
* Packets can arrive faster than OS can process
* [[Interrupts]] are very expensive
	* Involve a [[context switch]]
In worst case, can spend 100% of time in interrupt handler
* Never make any progress
* **Receive Livelock**
* 
