---
dg-publish: true
---
# Disk Performance
#### Placement and ordering of requests is a huge issue
* Sequential I/O much faster
* Long seeks are much slower than slower ones
Must be careful about order of crashes ([[Soft Updates]])
Try to achieve contiguous access ([[XFS]])

**Try to order requests to minimize seek time**
* Requires I/O concurrency
	* Handling multiple requests from multiple processes
	* 