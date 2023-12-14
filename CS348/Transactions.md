---
dg-publish: true
---
# Transactions

> [!tldr] Sequence of indivisible DML requests
> * Atomicity
> * Consistency
> * Isolation
> * Durability

#### Subsystems
* Concurrency Control Management
	* Responsible for scheduling the execution of reads and writes on physical objects in a way that ensures transaction isolation
* Recovery Management
	* Responsible for enduring transaction [[atomicity]] and durability


> [!info] DML processing is responsible for ensuring the part of the transaction consistency defined by the integrity constraints

Database is a finite set of independent physical objects $x_j$ that are read and written to transactions $T_i$
1. $r_i[x_j]$ - Transaction $T_i$ reads object $x_j$
2. $w_i[x_j]$ - Transaction $T_i$ writes object $x_j$

##### Transactions
$T_i$ is a sequence of read and write operations on a database
$T_i = r_i[x_1], r_i[x_2], w_i[x_1], …, r_i[x_4], w_i[x_2], c_i$
