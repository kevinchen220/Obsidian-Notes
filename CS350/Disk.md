---
dg-publish: true
---
# Disk
* Stack of [[Magnetic Platters]]
	* Rotate together on a central spindle @3600-15000 RPM
	* **Drive drifts slowly over time**
		* Cannot predict position after 100+ rotations
* Disk arm assembly
	* Arms rotate around pivot
		* All move together
	* Arms contain disk heads
		* one for each recording surface
		* Heads read data and write data to platters

## [[Disk positioning system]]
## [[Sectors]]

## [[Cost model for disk I⧸O]]
## [[Disk Interface]]
## [[Disk Performance]]

## Scheduling for Disks
### Approach 1: First come first served
#### Advantages
* Easy to implement
* Good fairness
#### Disadvantages
* Cannot exploit locality
* Higher latency → Lower throughput
### Approach 2: Shortest Positioning time first
Always pick request with shortest seek time
#### Advantages
* Exploits locality
* Higher throughput
#### Disadvantages
* Starvation
* Don’t always know what request will be fastest
### Approach 3: Elevator Scheduling (SCAN)
Like SPTF but next seek must be in same direction
* Switch directions only if no further requests
#### Advantages
* Locality
* Bounded waiting
#### Disadvantages
* Cylinders in middle of disk get better service
### VSCAN
Creates a continuum between SPTF and SCAN
* Like SPTF but introduce **effective positioning time**
If the request is same direction → $T_{eff} = T_{pos}$
Otherwise → $T_{eff} = T_{pos} + r* T_{max}$
* $T_{max}$ is maximum seek time
* Penalty for changing directions
**r is between 0 and 1**
* r=0 is SPTF
	* Just choose closest
* r=1 you get SCAN
	* Never change
* r=0.2 works well