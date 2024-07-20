---
dg-publish: true
---
# Reductions

> [!question] How do we prove problem $A$ is “easier than” another problem $B$

### Turing Reductions
* $A \leq_p^T B \iff$ there is a poly-time algorithm $M^B$ with oracle access to $B$ such that $M^B$ solves $A$
	* Oracle access: Algorithm $M^B$ can query the oracle on inputs to problem B, and each query is counted as 1 unit of time
### Karp Reductions
* $A \leq_p B \iff$ there is a poly-time computable function $f: A→ B$ such that
	* x is a YES instance of $A \iff f(x)$ is YES instance of $B$

### NP
1. [[NP-Completeness]]
2. [[NP-Hardness]]