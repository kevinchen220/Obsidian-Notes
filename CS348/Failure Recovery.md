---
dg-publish: true
---
# Failure Recovery
DBMS responsible for recovery management
1. Regarding [[atomicity]]: enable a transaction to be 
	1. Committed (With a guarantee database changes are permanent)
	2. Aborted (with a guarantee that there are no database changes)
2. Regarding reliability: Enable a database to be recovered to a consistent state in case of hardware or software failure

Interaction with recovery management
* Input: [[Two-Phase Locking|2PL]] and ACA schedule of operations produced by the transaction manager
* Output: Schedule of object rads, object writes, and object forced writes

> [!note] Approaches to Recovery
> 1. Shadowing
> 	1. Copy-on-write and merge-on-commit approaches
> 	2. Poor clustering
> 	3. Used in system $R$ but not in modern systems
> 2. Logging
> 	1. Uses log files on separate stable media
> 	2. Good utilization of buffers
> 	3. Preserves original clusters

## [[Logging]]
