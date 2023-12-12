# Relational Schema Good Design

> [!note] Relational Schema Diagnosis
> * **Usability**: How does a choice of design impact productivity?
> 	* Ease of expressing queries
> 	* Ease of expressing data revision
> 	* Metadata Transparency
> * **Resource requirements**: What are the allowed instances of the schema?

## Change Anomalies
![[Change Anomalies]]
### Fix
No more ambiguity
* Data revision is easier
* Query writing is harder but can be solved with views
![[Pasted image 20231212114108.png]]
### More example
Information is lost
* No references between tables
![[Pasted image 20231212114358.png]]
## [[Diagnosis and Repair]]