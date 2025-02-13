---
tags: cs456
dg-publish: true
---
# Control Plane
**Routing:** Determine route taken by packets from source to destination
* per-router control
* logically centralized control
#### Per-router Control Plane
Individual routing algorithm components in each and every router interact with each other in control plane to compute forwarding tables
![[Pasted image 20241216154637.png]]

#### Logically Centralized Control Plane
A distinct controller interacts with local control agents in routers to compute forwarding tables
![[Pasted image 20241216154855.png]]
## Routing Protocols
### Goal
Determine “good” paths from sending hosts to receiving hosts through network of routers
* **good:** least cost, fastest, least congested
### Classification
#### Global VS decentralized information
**Global:**
* All routers have complete topology, link cost info
* link state algorithm
**Decentralized:**
* Router knows physically-connected neighbors, link costs to neighbors, link costs to neighbors
* Iterative process of computation, exchange of info with neighbors
* distance vector algorithms
#### Static VS dynamic
**Static:**
* Routes change slowly over time
**Dynamic:**
* Routes change more quickly
	* Periodic update
	* In response to link cost changes

### Link State
#### [[Dijkstra’s Algorithm]]
* Net topology, link costs known to all nodes
	* Accomplished via “link state broadcast”
	* All nodes have same info
* Computes least cost paths from one node to all other nodes
* Iterative
	* after k iterations know least cost path to k destinations
**Complexity:** n nodes
* Each iteration: need to check all nodes, w, not in N
* n(n+1)/2 comparisons $O(n^2)$
	* $O(n\log n)$ possible
### Distance Vector
Node x only knows cost to each neighbor v
* From time to time, each node sends its own distance vector estimate to neighbors
#### [[Bellman-Ford Algorithm]] (DP)
![[Pasted image 20241216173031.png]]![[Pasted image 20241216173237.png]]
## Intra-AS Routing in the Internet: OSPF
### Making routing scalable
**Scale:** with billions of destinations
* can’t store all destinations in routing tables
* routing table exchange would swamp links!
**Administrative autonomy:**
* internet = network of networks
* each net5work admin may want to control routing in its own network
> [!important] Aggregate routers into regions known as “autonomous systems” (AS) (Domains)

## Intra-AS Routing
**AKA interior gateway protocol (IGP)**
* Routing among hosts, routers in same AS
* All routers in AS must run same intra-domain protocol
* Routers in different AS can run different intra-domain routing protocol
* Gateway router: at “edge” of its own AS, has links to routers in other AS’es
Most common intra-AS routing protocols:
* RIP: Routing Information Protocol
* OSPF: Open Shortedst Path First
* IGRP: Interior Gateway Routing Protocol
## Inter-AS Routing
* Routing among AS’es
* Gateways perform inter-domain routing
	* as well as intra-domain routing
### Tasks
1. Learn which destinations are reachable through other AS
2. Propagate this reachability info to all routers in AS
## Interconnected AS’es
* Forwarding table configured by both intra-AS and inter-AS routing algorithms
	* Intra-AS routing determine entries for destinations within AS
	* inter-AS and intra-AS determine entries for external destinations
## OSPF
**Open Shortest Path First**
* “Open”: publicly available
* Uses link-state algorithm
	* Link state packet dissemination
	* Topology map at each node
	* Uses Dijkstra’s algorithm
* Router floods OSPF link-state advertisements to all other routers in entire AS
	* Carried in OSPF messages directly over IP
* IS-IS routing protocol: nearly identical to OSPF
#### Advanced Features
* **Security:** all OSPF messages authenticated
* Multiple same-cost paths allowed
* For each link, multiple cost metrics for different types of service
	* satellite link cost low for best effort ToS, high for real-time ToS
##### Hierarchical OSPF
* **Two-level hierarchy:** local area, backbone
	* Link-state advertisements only in area
	* Each nodes has detailed area topology; only know shortest paths to nets in other areas
* **Area border routers:** summarize distances to nets in own area, advertise to other Area Border routers
* **Backbone routers:** run OSPF routing limited to backbone
* **Boundary routers:** connect to other AS’es
![[Pasted image 20241216194816.png]]

## BGP
**Border Gateway Protocol**
> [!tldr] Inter-AS routing

BGP provides each AS a means to:
* **eBGP:** obtain subnet reachability information from neighboring AS’es
* **iBGP:** propagate reachability to all AS-internal routers
* determine good routes to other networks based on reachability information and policy
![[Pasted image 20241216195320.png]]
**BGP Session:** Two BGP routers exchange BGP messages over semi-permanent TCP connection
* Advertising paths to different destination network prefixes
> [!example]
> When AS3 gateway router 3a advertises path AS3,X to AS2 gateway router 2c:
> * AS3 promises to AS2 it will forward datagrams towards X
> 
> ![[Pasted image 20241216195559.png]]

### Path Attributes and BGP Routes
Advertised prefix includes BGP attributes
* prefix + attributes = “route”
Two important attributes:
* **AS-PATH:** list of AS’es through which prefix advertisement has passed
* **NEXT-HOP:** indicates specific internal-AS router to next-hop AS
*Policy-based routing:*
* Gateway receiving route advertisement uses import policy to accept/decline path
* AS policy also determines whether to advertise path to other neighboring AS’es
> [!example]-
> ![[Pasted image 20241216195931.png]]
> #### Multiple paths
> ![[Pasted image 20241216200101.png]]

### BGP Messages
BSP messages exchanged between peers over TCP connection
* **OPEN:** opens TCP connection to remote BGP peer and authenticates sending BGP peer
* **UPDATE:** advertises new path
* **KEEPALIVE:** keeps connections alive in absence of UPDATES; also ACKs OPEN request
* **NOTIFICATION:** reports errors in previous msg; also used to close connection
![[Pasted image 20241216201204.png]]
### BGP Route Selection
Router may learn about more than one route to destination AS, selects route based on:
1. Local preference value attribute: policy decision
2. Shortest AS-PATH
3. closest NEXT-HOP router: hot potato routing
4. additional criteria
#### Hot Potato Routing
Chooses local gateway that has least intra-domain cost
* Don’t worry about inter-domain cost
![[Pasted image 20241216201529.png]]
#### Achieving Policy via Advertisements
B only wants to route traffic to/from its customer networks
* Does not want to carry transit traffic between other ISPs
![[Pasted image 20241216202029.png]]
## Why different Intra-AS, Inter-AS Routing?
**Policy:**
* Inter-AS: admin wants control over how its traffic is routed, who routes through its net
* Intra-AS: single admin, so no policy decisions  needed
**Scale:**
* Hierarchical routing saves table size, reduced update traffic
**Performance:**
* Intra-AS: can focus on performance
* Inter-AS: policy can dominate over performance

## Software Defined Networking (SDN)
#### Why a logically centralized control plane?
* Easier network management
	* Avoid router misconfigurations, greater flexibility of traffic flows
	* Table-based forwarding allows programming routers
		* Centralized programming easier: compute tables centrally and distribute
		* Distributed programming: more difficult
	* Open implementation of control plane
![[Pasted image 20241216215232.png]]
#### Data Plane Switches
![[Pasted image 20241216215604.png]]
* Fast, simple, commodity switches implementing generalized data-plane forwarding in hardware
* Switch flow table computed, installed by controller
* API for table-based switch control
* Protocol for communicating with controller
#### SDN Controller
![[Pasted image 20241216215611.png]]
* Maintain networks state information
* Interacts with network control applications via northbound API
* Interacts with network switches via southbound API
* Implemented distributed system for performance, scalability, fault-tolerance, robustness
![[Pasted image 20241216215909.png]]
#### Network-control Apps
![[Pasted image 20241216215701.png]]
* Brains of control
	* implement control functions using lower level services, API provided by SDN controller
* Unbundled: can be provided by third party