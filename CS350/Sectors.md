---
dg-publish: true
---
# Sectors

> [!tldr] The disk interface typically represents the disk as a linear array of blocks
> Disk maps logical locations to physical sectors

#### Disk maps logical locations to physical locations
**Zoning**
* Puts more sectors on larger tracks
	* Outside tracks with larger radius
**Track skewing**
* Sector 0 position varies by track to improve sequential access time
**Sparing**
* Flawed sectors are remapped to locations
#### OS doesn’t know logical to physical mapping
* Larger logical number difference means larger seek times
	* Non-linear
	* Depends on zone
