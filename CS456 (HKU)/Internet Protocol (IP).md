---
tags:
  - cs456
dg-publish: true
---
# Internet Protocol (IP)
## IP Datagram Format
![[Pasted image 20241214150611.png]]
## IP Fragmentation and Reassembly
![[Pasted image 20241214150751.png]]
* Network links have MTU (Max transfer size)
	* Largest possible link-level frame
* Large IP datagram divided within net
	* Reassembled only at final destination
	* IP header bits used to identify, order related fragments
![[Pasted image 20241214150847.png]]

## IPv4 Addressing
**IP address:** 32-bit identifier for host, router interface
**Interface:** Connection between host/router and physical link
* Routers typically have multiple interfaces
* Host typically has one or two interfaces
*IP address associated with each interface*
![[Pasted image 20241214151402.png]]
#### How are interfaces connected?
[[Link Layer]]
![[Pasted image 20241214151435.png]]
## Subnets
Device interfaces with same subnet part of IP address
* Can physically reach each other without intervening router
![[Pasted image 20241214151813.png]]
> [!tldr] High order bits of IP address is subnet part, low order bits are host part
#### CIDR: Classless InterDomain Routing
* Subnet portion of address of arbitrary length
* Address format: **a.b.c.d/x**, where x is # bits in subnet portion of address
![[Pasted image 20241214152023.png]]
### DHCP: Dynamic Host Configuration Protocol
> [!faq] How does a host get IP address
> Dynamically get address from a server

Allow host to dynamically obtain its Ip address from network server when it joins network
* can renew its lease on address in use
* allow reus of addresses
* support for mobile users who want to join netowrk
##### Steps
1. Host broadcasts **DHCP discover** msg (optional)
2. DHCP server responds with **DHCP offer** msg (optional)
3. Host requests IP address: **DHCP request**
4. DHCP server sends address: **DHCP ack**
![[Pasted image 20241214152705.png]]
DHCP can return more than just allocated IP address on subnet:
* Address of first-hop router for client
* Name and IP address of DNS server
* Network mask
#### Hierarchical Addressing: route aggregation
Allows for efficient advertisement of routing information
![[Pasted image 20241214153148.png]]

## IPv6
#### Motivation
32-bit address space soon to be completely allocated
Header format helps speed processing/forwarding
Header changes to faciliate QoS
### Format
* Fixed-length 40 byte header
* No fragmentation allowed
![[Pasted image 20241214155943.png]]
##### Differences to IPv4
* Removed checksum
* Options: available as upper-layer, next-header protocol at router
* ICMPv6

#### Transition from IPv4 to IPv6
![[Pasted image 20241214160223.png]]
**Tunneling:** IPv6 datagram carried as payload in IPv4 datagram among IPv4 routers
![[Pasted image 20241214160252.png]]

