---
dg-publish: true
---
# Logging
Read/append only data structure on stable media
→ Recovery manager appends transaction log records
→ Aborting and failure recovery reads transaction log records

* **UNDO:** Old version of objects that have been modified by a transaction
	* Can be used to undo database changes on abort
* **REDO:** New versions of objects that have been modified by a transaction
	* Can be used to redo the work done by a transaction that commits
* **BEGIN/COMMIT/ABORT:** Record when transactions begin, commit, or abort

### Example
Five transactions: $\{T_0, T_1, T_2, T_3, T_4\}$
Transaction status
* $\{T_1, T_3\}$ committed
* $\{T_2\}$ aborted
* $\{T_0, T_4\}$ active

![[Pasted image 20231214095333.png]]

### Write-Ahead Logging

> [!warning] Allowing indices on stable store to be updated prior to a LOG can lead to inconsistency
#### Undo Rule
Log record for an update is appended to the LOG file before the corresponding data page is written to stable store
→ Guarantees [[atomicity]]
#### Redo Rule
All log records for a transaction are appended to the LOG file before acknowledging a commit
→ Guarantees durability

