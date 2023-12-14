---
dg-publish: true
---
# Disk Interface
* Disk controller controls the hardware and mediate access
* Processor and disk are often connected by [[bus]]
	* Multiple devices contend for the bus
#### Features
Disconnect from bus during request
**Command queueing**
* Give disk multiple requests
* Disk can make scheduling decisions using current position of read/write head
Disk cache used for **read-ahead**
* Assuming sequential reads
**Write caching**
* Don’t write everytime
* Cache some writes and write together later

### [[SCSI]] - Small Computer System Interface

