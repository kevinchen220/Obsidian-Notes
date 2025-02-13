---
tags: cs456
dg-publish: true
---
# Network Address Translation (NAT)
![[Pasted image 20241214153408.png]]
> [!important] Motivation
> Local network uses just one IP address as far as outside world is concerned:
> * Range of addresses not needed from ISP
> 	* Just one IP address for all devices
> * Can change addresses of devices in local network without notifying outside world
> * Can change ISP without changing addresses of devices in local network
> * Devices inside local net not explicitly addressable
> 	* Visible by outside world

## Implementation
NAT router must:
* **Outgoing datagrams:** Replace (source IP address, port #) of every outgoing datagram to (NAT IP address, new port #)
	* Remote clients/servers will respond using (NAT IP address, new port #) as destination addr
* **Remember (in NAT translation table)** every (source IP address, port #) to (NAT IP address, ,new port #) translation pair
* **Incoming datagrams:** Replace (NAT IP address, new port #) in dest fields of every incoming datagram with corresponding (source IP address, port #) stored in NAT table
![[Pasted image 20241214154316.png]]
