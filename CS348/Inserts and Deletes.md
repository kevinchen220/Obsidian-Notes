---
dg-publish: true
---
# Inserts and Deletes

> [!warning] DML processing requires creating or deleting physical objects
> Neither 2PL nor strict 2PL correctly handles such cases

### Phantom Tuple Problem
1. Based on sufficient fixed budget, transaction $T_1$ gives each employee a bonus
2. As a consequence of a new hire, transaction $T_2$ adds a new employee who should not receive a bonus
	* New employee appears as $T_1$ is executing

> [!success] Resolution
> DML requests that modify the database according to the results of a query need larger scale locks
> * Lock on entire indices
> * Predicate locks on tables
> 	* **Coarse grained lock:** Exclusive lock on entire table
> 	* **Fine grained lock:** Lock on tuple or row
> * Appropriate lock compatibility rules




