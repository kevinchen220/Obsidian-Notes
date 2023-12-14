---
dg-publish: true
---
# Concurrency Control

> [!NOTE] Basics of Transaction Processing
> DML processing converts interaction with sets of tuples to a sequence of operations that read and write physical objects in the database
> * Database objects
> 	* Individual record files
> 	* Records
> 	* Physical pages
> 	* Entire files
> 	* Predicates qualifying one or more records, parts of records, etc
> * Transaction and recovery management
> 	* Ensuring correct and concurrent execution of operations for reading and writing physical objects originating from DML commands of client transactions
> 	* Guaranteeing that acknowledged client transaction commits are reliably recorded and that acknowledged client transaction aborts are reliably undone

### [[Transactions]]
### [[Schedules]]

> [!info] Other Properties
> **Recoverable Schedules**
> * Allow committing only in order of the read-from dependency between transactions
> 	* *Conflicting operations must be committed in the same order they are performed*
> 
> **Cascadeless Schedules**
> * Do not allow transactions to read uncommitted objects
> 	* *Can only read a write if it is committed*


