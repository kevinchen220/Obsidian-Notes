---
tags:
  - cs456
  - unit
dg-publish: true
---
# Link Layer
Datagram transferred by different link protocols over different links
* Each link protocol provides different services
> [!example] Analogy
> * Trip from Princeton to Lausanne
> 	* Car: Princeton to JFK
> 	* Plane: JFK to Geneva
> 	* Train: Geneva to Lausanne
> * tourist = **datagram**
> * transport segment = **communication link**
> * transportation mode = **link layer protocol**
> * travel agent = **routing algorithm**

### Link Layer Services
**Framing, Link Access:**
* Encapsulate datagram into frame, adding header, trailer
* Channel access if shared medium
* MAC addresses used in frame headers to identify source, destination
**Reliable delivery between adjacent nodes:**
**Flow Control:**
* Pacing between adjacent sending and receiving nodes
**Error Detection:**
* Errors caused by signal attenuation, noise
* Receiver detects presence of errors:
	* Signals sender for retransmission or dops frame
**Error Correction:**
* Receiver identifies and corrects bit errors without resorting to retransmission
**Half-duplex and full-duplex**
* With half duplex, nodes at both ends of link can transmit, but not at same time

#### Where is the link layer implemented
* In each and every host
* link layer implemented in adaptor or on a chip
	* Ethernet card, 802.1.1 card
	* Implements link, physical layer
* Attaches into host’s machine
* Combination of hardware, software, firmware
### Adaptors Communicating
**Sending Side:**
* Encapsulates datagram in frame
* Adds error checking bits, rtd, flow control, etc.
**Receiving Side:**
* Looks for errors, rdt, flow control, etc.
* Extracts datagram, passes to upper layer at receiving side

## Error Detection
![[Pasted image 20241216234301.png]]
EDC = Error Detection and Correction bits (redundancy)
D = Data protected by error checking, may include header fields
* Error detection not 100% reliable
	* Protocol may miss some errors, but rarely
	* Larger EDC field yields better detection and correction
## Parity Checking
#### Single bit parity:
![[Pasted image 20241216234731.png]]
* Detect single bit errors
#### Two-dimensional bit parity:
![[Pasted image 20241216234804.png]]
* Detect and correct single bit errors
#### Internet Checksum
**Goal:** detect “errors” in transmitted packet
* Used in transport layer only

## Cyclic Redundancy Check
* More powerful error-detection coding
* View data bits, **D**, as a binary number
* Choose r+1 bit pattern, **G**
* Goal: choose r CRC bits, **R**, such that
	* <D,R> exactly divisible by G (modulo 2)
	* Receiver knows G, divides <D,R> by G. If non-zero remainder: ERROR DETECTED!
	* Can detect all burst errors less that r+1 bits
![[Pasted image 20241219122114.png]]
#### Example
![[Pasted image 20241219122144.png]]
## Multiple Access Protocols
**Single shared broadcast channel**
* Collision if node receives two or more signals at the same time
> [!tldr] Distributed algorithm that determines how nodes share channel
> * Determine how nodes share channel
> * Communication about channel sharing must use channel itself

Two types of links:
* Point-to-point:
	* PPP for dial-up access
	* Point-to-point link between Ethernet switch, host
* Broadcast (shared wire or medium)
	* Old-fashioned Ethernet
	* Upstream HFC
	* 802.1 1 wireless LAN
## Random Access Protocols
* When node has packet to send
	* Transmit at full channel data rate R
	* No prior coordination among nodes
* Two or more transmitting nodes → Collision
* random access MAC protocol specifies:
	* How to detect collisions
	* How to recover from collisions
### Slotted ALOHA
#### Assumptions
* All frames same size
* Time divided into equal size slots
	* Time to transmit 1 frame
* Nodes start to transmit only slot beginning
* Nodes are synchronized
* If 2 or more nodes transmit in slot, all nodes detect collision
#### Operations
* When node obtains fresh frame, transmits in  next slot
	* if no collision:
		* Node can send new frame in next slot
	* if collision:
		* Node retransmits frame in each subsequent slot with probability p until success
![[Pasted image 20241219140018.png]]
#### Pros
* Single active node can continuously transmit at full rate of channel
* Highly decentralized: only slots in nodes need to be in sync
* Simple
#### Cons
* Collisions, wasting slots
* idle slots
* Nodes may be able to detect collision in less than time to transmit packet
* Clock synchronization
#### Efficiency
**At best, channel used for useful transmission 37% of time**
$$Np(1-p)^{N-1}$$
$N$ is number of nodes
$p$ is probability of transmission
### Pure ALOHA
Simpler, no synchronization
* When frame first arrives
	* Transmit immediately
* Collision probability increases
	* frame sent at $t_0$ collides with other frames sent in $[t_0-1,t_0+1]$
![[Pasted image 20241219140626.png]]
#### Efficiency
$$Np(1-p)^{2(N-1)}$$$N$ is number of nodes
$p$ is probability of transmission

### CSMA
**Carrier Sense Multiple Access**
* Listen before transmit
	* If channel sensed idle: transmit entire frame
	* If channel sensed busy: defer transmission
#### Collisions
Propagation delay:
* Two nodes may not hear each other’s transmission
Collision:
* Entire packet transmission time wasted
	* Distance & propagation delay play role in determining collision probability
### CSMA/CD (collision detection)
Carrier sensing, deferral as in CSMA
* Collisions detected within short time
* Colliding transmissions aborted, reducing channel wastage
**Collision detection:**
* Easy in wired LANs: Measure signal strengths, compare transmitted, received signals
* Difficult in wireless LANs: received signal strength overwhelmed by local transmission strength
![[Pasted image 20241219143635.png]]
#### Ethernet CSMA/CD Algorithm
1. NIC receives datagram from network layer, creates frame
2. If NIC senses channel idle, starts frame transmission
3. If NIC senses channel busy, waits until channel idle, then transmits
4. If NIC transmits entire frame without detecting another transmission, NIC is done with frame
5. If NIC detects another transmission while transmitting, aborts and sends jam signal
6. After aborting, NIC enters binary backoff
	1. After $m$th collision, NIC chooses $K$ at random from {0,1,2, …, $2^m-1$}}
	2. NIC waits $K\times 512$ bit times
	3. Return to step 2
#### Efficiency
$t_{\text{prop}}$ = max prop delay between 2 nodes in LAN
$t_{\text{trans}}$ = time to transmit max-size frame
$$\text{efficiency} = \frac{1}{1+5t_{\text{prop}}/t_{\text{trans}}}$$
Efficiency goes to 1
* as $t_{\text{prop}}$ goes to 0
* as $t_{\text{trans}}$ goes to $\infty$
Better performance than ALOHA
* Simple
* Cheap
* Decentralized

### Taking turns MAC protocols
* Polling
	* Master and slave nodes
* Token passing
	* control token passed from one node to next
## MAC addresses and ARP
32-bit IP address:
* network-layer address for interface
* used for network layer forwarding
* Not portable (postal code)
### MAC Address:
**Used locally to get frame from one interface to another physically-connected interface**
* 48-bit MAC address burned in NIC ROM, also sometimes software settable
* e.g. 1A-2F-BB-76-09-AD
	* hexadecimal, each numeral is 4 bits
* Portable (SSN)
### ARP (Address resolution protocol)
Each IP node on LAN has table
* IP/MAC address mappings for some LAN nodes
	* <IP address; MAC address; TTL>
* TTL (Time to Live):
	* Time after which address mapping will be forgotten
	* Typically 20 min

## Switch
Link-layer device:
* store, forward Ethernet frames
* examine incoming frame’s MAC address, selectively forward frame to one-or-more outgoing links when frame is to be forwarded on segment
	* Uses CSMA/CD to access segment
Transparent:
* Hosts are unaware of presence of switches
Plug-and-play, self-learning:
* Switches do not need to be configured
### Switch forwarding table
Each switch has a switch table with entries:
* (MAC address of host, interface to reach host, time stamp)
> [!faq] How are entries created, maintained in switch table?
> Self-learning
> * Switch learns which hosts can be reached through which interfaces
> 	* When frame received, switch learns location of sender: incoming LAN segment
> 	* Records sender/location pair in switch table

**If location unknown, flood**
* Forward on all interfaces except arriving interface

### Switches VS. Routers
Both are store-and-forward:
* Routers: network-layer devices
* Switches: link-layer devices
Both have forwarding tables:
* Routers: Compute tables using routing algorithms, IP addresses
* Switches: Learn forwarding table using flooding, learning, MAC addresses