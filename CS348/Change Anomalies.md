---
dg-publish: true
---
# Change Anomalies

> [!tldr] Inconsistencies that result from an operation like update, insertion, or deletion

> [!example] 
> ![[Pasted image 20231212113731.png]]
> No clear problem with expressing queries
> **Problems with data revisions**
> * Update
> 	* Change name of supplier S1 to ACME
> 	* *Need to change all S1*
> * Insert
> 	* Add item I4 with name Washer
> 	* *What about the first 3 columns?*
> * Delete
> 	* Supplier “Budd” no longer supplies screws
> 	* *Do we delete Budd or just the screws?*
