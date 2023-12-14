---
dg-publish: true
---
# Diagnosis and Repair
### Appeal to the integrity constraints of a relational database schema
* Integrity constraints can imply regularities in database instances that lead to [[change anomalies]]
* Possible repair is to replace a table by two or more other tables
## Decomposition
Assume a relation schema is given by a set of [[attributes]] $\{A_1, ... , A_k\}$, let $R$ be a relational schema and $\{R_1, …, R_n\}$ be a set of $n$ relational schemata
Then  $\{R_1, …, R_n\}$ is a **decomposition** of $R$ if $$R = \bigcup_{1\leq i\leq n}R_i$$
> [!tip] Integrity constraints can determine that a decomposition does not lose information


