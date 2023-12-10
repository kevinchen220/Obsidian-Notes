# Multicore Caches

> [!tldr] Performance requires multilevel caches since access to RAM is slow

> [!warning] Multiple caches may cause different caches to disagree on memory locations

## Bus-based approaches
* Each core listens to memory bus
* The core writing the value write through caching and the other cores invalidate their values for that memory location when they see a write to the same adderss
## Network-based approach
* hypertransport (older AMD), Infinity Fabric (newer AMD), UPI (Intel)

## Cache lines
* Typically 64 bytes
* Amount of data that is transferred to different caches or main memory
	* Take advantage of locality of reference