---
tags: cs456
---
# Generalized Forwarding
> [!tldr] Each router contains a flow table that is computed and distributed by a logically centralized routing controller
> ![[Pasted image 20241214160425.png]]

## OpenFlow
**Flow:** Defined by header fields
**Generalized Forwarding:** Simple packet-handling rules
* Pattern: match values in packet header fields
* Actions: for matched packet: drop, forward, modify, send matched packet to controller
* Counters: # bytes and # packets
![[Pasted image 20241214160644.png]]
