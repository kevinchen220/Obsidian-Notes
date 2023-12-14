---
dg-publish: true
---
# Journaling

> [!warning] 
> Biggest crash-recovery challenge is inconsistency
> * one logical operation requires multiple separate disk writes
> * If only some happen, could cause a lot of problems
> 
> **Most of these problematic writes are to metadata**

## Idea
Use a **write-ahead** log to **journal** metadata
* Reserve a portion of disk for a log
* Write any metadata operation first to the log, then make the change on the disk
* After crash/reboot, replay the log
	* May redo already committed changes but won’t miss anything


> [!tip] Group multiple operations into one log entry
> 
### Performance advantage
* The log is a consecutive portion of a disk
* Multiple operations can be logged at disk bandwidth

## Details
#### Challenge
Find oldest relevant log entry
- Other wise redundant and slow to go over entire log
**Use checkpoints**
* Never need to go back before most recent checkpointed N
Must also find the end of the log
* A circular buffer
* Can include begin transaction and end transaction