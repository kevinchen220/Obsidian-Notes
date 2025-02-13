---
tags:
  - cs456
---
# Packet Scheduling
## First Come First Serve
Packets transmitted in order of arrival
* Queue

## Priority
Arriving traffic classified, queued by class
* Send packet from highest priority queue that has buffered packets
![[Pasted image 20241214150000.png]]

## Round Robin
Arriving traffic classified, queued by class
* Server cyclically, repeatedly scans class queues, sending one complete packet from each class in turn 
![[Pasted image 20241214150218.png]]

## Weighted Fair Queueing
* Generalized round robin
* each class, $i$, has weight, $w_i$, and gets weighted amount of service in each cycle
$$\frac{w_i}{\sum_j{w_j}}$$
![[Pasted image 20241214150357.png]]
> [!important] Any header fields can be used for classification for priority, class, etc.

