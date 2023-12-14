---
dg-publish: true
---
# Schedules

> [!tldr] For a set of transactions $\{T_1, … T_k\}$ produces an execution order of operations $S$ such that
> 1. Every operation $o_i \in T_i$ appears also in $S$
> 2. $T_i$‘s operations in $S$ are ordered the same way as in $T_i$


> [!success] Goal
> Produce a correct schedule with maximal parallelism

If $T_i$ and $T_j$ are concurrent transactions, then it is always correct to schedule the operations in such way that
1. $T_i$ will appear to precede $T_j$
	1. $T_j$ will see all updates made by $T_i$
	2. $T_i$ will not see any updates made by $T_j$
2. $T_i$ will appear to follow $T_j$
	1. $T_i$ will see $T_j$‘s updates
	2. $T_j$ will not see $T_i$‘s updates

**Correct:** Schedule appears to clients that the transactions are executed sequentially

### Serializable Schedules
Equivalent to some serial execution of the same transactions

#### Conflict Equivalence
All conflicting operations for two schedules are ordered the same way

Two operations **conflict** if they
1. Belong to different [[transactions]]
2. Access the same data item $x$
3. At least one of them is a write operation $w[x]$

Schedule $S_1$ is a **conflict serializable schedule** if it is conflict equivalent to some serial schedule $S_2$

> [!info] View Equivalence
> Preserves initial reads and final writes
> 1. Allows more schedules
> 2. Is NP-hard to diagnose

#### Serialization Graph
$SG(N,E)$ for a schedule $S$ is a directed graph
1. Nodes $T_i\in N$ corresponding to the transactions of $S$
2. Edges $T_i→T_j \in E$ whenever an operation $o_i[x]$ for transaction $T_i$ occurs prior $o_j[x]$ for transaction $T_j$ in $S$, where $o_i[x]$ and $o_j[x]$ are **conflicting operations**

**Theorem:** Schedule $S$ is serializable if and only if the serialization graph $SG$ for $S$ is acyclic




