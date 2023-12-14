---
dg-publish: true
---
# Minimal Cover

> [!info] Two sets of [[functional dependencies]] $F$ and $G$ are equivalent if and only if $F^+=G^+$

Set of dependencies $F$ is **minimal** if it satisfies the following conditions:
1. Every right-hand side of a dependency in $F$ is a single attribute
2. For no $X→A$ is the set $F-\{X→A\}$ equivalent to $F$
3.  For no $X→A$ and $Z \subset X$ is the set $F-\{X→A\} \bigcup \{Z→A\}$ equivalent to $F$

##### Theorem
For every set of dependencies $F$ there is an equivalent minimal set of dependencies called a **minimal cover**
#### Computation
Given a set of function dependencies apply each step until it no longer succeeds in updating $F$
1. Replace $X→YZ$ with the pair $X→Y$ and $X→Z$ 
2. Replace $X→A$ from $F$ if $A\in computeX^+(X, F-\{X→A\})$ 
3. Remove $A$ from left-hand side of $X→B$ in $F$ if $B$ is in $computeX^+(X-\{A\}, F)$
4. Replace $X→Y$, $X→Z$ in $F$ by $X→YZ$

