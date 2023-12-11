# Cost model for disk I⧸O
#### The time it takes to move data to/from a disk involves
1. Seek time
	* The time it takes to move the read/write heads to the appropriate [[tracks|track]]
		* Depends on seek distance
		* Values range from 0ms to max seek time
2. Rotational latency
	* The time it takes for the desired sectors spin to the read/write heads
		* Depends on rotational speed of disk
		* Value range from 0ms to time for single rotation
3. Transfer time
	* The time it takes until the desired sectors spin under the read/write heads
		* Depends on the rotational speed of the disk
		* Amount of data accessed
**Request service time = Seek time + Rotational latency + Transfer time**

> [!example] 
> Parameters
> * Disk capacity: $2^{32}$ bytes
> * Number of tracks: $2^{20}$ tracks per surface
> * Number of sectors per Track: $2^8$ sectors
> * Rotations per Minute: 10000RPM
> * Maximum seek time: 30ms

**How many bytes are in a track?**
* Bytes per track = Disk capacity / num tracks = $2^{32} / 2^{20} = 2^{12}$

**How many bytes per sector?**
* Bytes per sector = bytes per track / number of sectors = $2^{12} / 2^8 = 2^4$

**What is the maximum rotational latency?**
* Max latency = 60 / RPM = 60 / 10000 = 6ms

**What is the average seek time?**
* Average seek = max seek / 3 = 30 / 3 = 10ms

**What is the average rotational latency assuming a uniform distribution?**
* Average latency = Max latency / 2 = 6 / 2 = 3ms

**What is the cost to transfer 1 sector?**
* Sector latency = Max latency / num sectors per track = 6 / $2^8$ = 0.0234 ms per sector

**What is the expected cost to read 10 consecutive sectors**
* Average seek + average rotational latency + Transfer time = 10 + 3 + 10 * 0.0234= 13.234ms
