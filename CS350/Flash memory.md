---
dg-publish: true
---
# Flash memory
### Completely solid state
No moving parts
* remember data by storing charge
* Lower power consumption and heat
* No mechanical seek times to worry about
##### Limitations
**Limited number of overwrites possible**
* Blocks wear out after 10000-100000 erases
* Requires flash translation layer (FTL) to provide wear levelling
	* Repeated writes to logical block don’t wear out physical block
	* Even out wear
	* FTL can seriously impact performance
**Limited durability**
* Charge wears out over time
* Can lose data if power off for a year

## [[Types of flash memory]]