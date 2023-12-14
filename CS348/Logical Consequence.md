---
dg-publish: true
---
# Logical Consequence
### [[Functional Dependencies|Functional Dependency]] Closure
Given a relation $R$ with [[attributes]] $\{A_1, ... , A_k\}$ and a set $F \cup \{X→Y\}$ of functional dependencies over $R$
$F$ logically implies $X→Y$ whenever $X→Y$ holds in all instances of $R$ that satisfies each FD in $F$
The **closure** $F^+$ of $F$ is the set of all functional dependencies that are logically implied by $F$

> [!NOTE] **Observation:** $F \subseteq F^+$
> If $F = \{A→B, B→C\}$ then
> $\{A→B, B→C, A→C\} \subseteq F^+$

