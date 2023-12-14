---
dg-publish: true
---
# Deadlocks
Sequence of transaction $(T_1, …, T_n)$ where $T_i$ must wait for $T_{i+1}$ to release locks, $1 \leq i < n$, and where $T_n$ must wait for $T_1$ to release locks

> [!example] 
> $r_1[x], r_2[y], w_2[x], w_1[y]$
> * $w_2[x]$ is blocked by $T_1$
> * $w_1[y]$ is blocked by $T_2$

## Prevention
#### Deadlock Prevention (Active)
* Locks granted only if they can’t lead to a deadlock
* All other objects are ordered and locks granted in this order
#### Deadlock detection (Passive)
* Use wait for graphs and cycle detection
* System aborts one of the offending transactions







similar to [[Deadlock]] from CS 350

